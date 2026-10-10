---
title: "Track Alias in the Data Plane for Media over QUIC Transport"
abbrev: "moq-track-alias"
category: std

docname: draft-frindell-moq-track-alias-latest
submissiontype: IETF
number:
date:
consensus: true
v: 3
ipr: trust200902
area: "Web and Internet Transport"
workgroup: "Media Over QUIC"
keyword:
 - media over quic
 - track alias
venue:
  group: "Media Over QUIC"
  type: "Working Group"
  mail: "moq@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/moq/"
  github: "afrind/draft-frindell-moq-track-alias"
  latest: "https://afrind.github.io/draft-frindell-moq-track-alias/draft-frindell-moq-track-alias.html"

stand_alone: yes
smart_quotes: no
pi: [toc, sortrefs, symrefs, docmapping]

author:
  -
    ins: A. Frindell
    name: Alan Frindell
    organization: Meta
    email: afrind@meta.com
    role: editor

normative:
  MOQT: I-D.ietf-moq-transport

--- abstract

This document defines an extension to Media over QUIC Transport (MOQT) that lets
a publisher identify Subgroups and Datagrams by the Track's TRACK_ALIAS Property
instead of the subscription's Request ID. It defines a Setup Option to negotiate
the extension and a modified encoding of the identifier field in SUBGROUP_HEADER
and OBJECT_DATAGRAM.

--- middle

# Introduction

MOQT {{MOQT}} identifies the subscription that a Subgroup or Datagram belongs to
by the Request ID of the SUBSCRIBE or PUBLISH that initiated it. Request IDs are
specific to a session, so a relay forwarding an Object to many subscribers
rewrites the header for each one, and a receiver cannot associate data with a
Track until it knows the Request ID.

The TRACK_ALIAS Track Property ({{MOQT}}) carries a numeric identifier that is
unique within the MOQT scope. This extension lets a publisher put that value in
the data plane, so headers for a Track are identical on every session that
negotiates the extension.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

This document uses the terminology and wire format notation of {{MOQT}}.

# Extension Negotiation {#negotiation}

An endpoint indicates support for this extension by including the
TRACK_ALIAS_DATA Setup Option in its SETUP message.

~~~
TRACK_ALIAS_DATA Setup Option {
  Option Type (vi64) = 0x0D,
  Length (vi64) = 0,
}
~~~
{: #track-alias-data-format title="TRACK_ALIAS_DATA Setup Option"}

When an endpoint receives a TRACK_ALIAS_DATA Setup Option with a non-zero
Length, it MUST close the session with a `KEY_VALUE_FORMATTING_ERROR`.

The extension is negotiated when an endpoint has both sent and received this
option, per the extension negotiation described in {{MOQT}}. It applies to both
directions of the session.

Because negotiation changes the encoding of data streams and datagrams
({{data-id}}), an endpoint that offers this extension MUST NOT send a
SUBGROUP_HEADER or OBJECT_DATAGRAM until it has received the peer's SETUP.

This extension relies on TRACK_ALIAS being unique among the Tracks in a session,
so it is only used when all of them belong to the same MOQT scope.

This extension can be used with versions of {{MOQT}} that identify subscriptions
in data by Request ID and define the TRACK_ALIAS Track Property.

# Data ID {#data-id}

When the extension is negotiated, the Request ID field of SUBGROUP_HEADER and
OBJECT_DATAGRAM is replaced by a Data ID:

~~~
SUBGROUP_HEADER {
  Type Flags (vi64),
  Data ID (vi64),
  Group ID (vi64),
  [Subgroup ID (vi64),]
  [Publisher Priority (8),]
}

OBJECT_DATAGRAM {
  Type Flags (vi64),
  Data ID (vi64),
  Group ID (vi64),
  ...
}
~~~
{: #data-id-format title="SUBGROUP_HEADER and OBJECT_DATAGRAM with Data ID"}

The least significant bit of Data ID indicates how the remaining bits identify
the subscription:

* 0: Data ID is the Request ID shifted left by one bit, as in {{MOQT}}.

* 1: Data ID is the TRACK_ALIAS shifted left by one bit, plus one.

For example, Request ID 4 is encoded as Data ID 8, and TRACK_ALIAS 4 is encoded
as Data ID 9. A Request ID or TRACK_ALIAS of 2^63 or greater cannot be encoded;
a publisher uses the Request ID form for a Track whose TRACK_ALIAS is too large.

FETCH_HEADER is unchanged.

# Using Track Alias {#using}

A publisher MAY identify a subscription's data by Track Alias if the Track
Properties in the PUBLISH or SUBSCRIBE_OK for that subscription include
TRACK_ALIAS. A publisher MAY identify some of a subscription's data by Request
ID and the rest by Track Alias.

When an Object matches the filters of multiple subscriptions to the same Track,
the publisher MUST send the Object once for each matching subscription, even
when those subscriptions share the same Track Alias. Because subscriptions can
share a Track Alias, the subscriber re-applies each subscription's filter to
determine which subscription a received Object belongs to.

Because TRACK_ALIAS is unique within the MOQT scope, a Track Alias never refers
to two different Tracks in a session. If a subscriber receives a PUBLISH or
SUBSCRIBE_OK that uses the same Track Alias as a different Track with an
`Established` subscription, it MUST close the session with error
`DUPLICATE_TRACK_ALIAS`.

Objects can be sent before the Subscriber knows the Track Alias, requiring
buffering Objects with an unknown Track Alias. If a Track Alias is used for two
concurrent subscriptions to the same Track, an Object that arrives with the
Track Alias could be for either Subscription. Reusing the same Track Alias for
concurrent subscriptions to the same Track can lead to missed delivery if
objects for the new subscription arrive before the control message establishing
the shared Alias. The Subscriber can assume the Track Alias is reused until told
otherwise, in order to avoid missing Objects.

The rules in {{MOQT}} for data with an unknown Request ID, and for Objects
that arrive after a subscription has been cancelled, also apply to Track
Aliases. A Track Alias is unknown until the PUBLISH or SUBSCRIBE_OK that carries
it arrives, so unlike a Request ID, it can be unknown for a SUBSCRIBE the
subscriber sent.

# Relays {#relays}

This extension is negotiated hop-by-hop, but the TRACK_ALIAS Track Property is
end-to-end: Relays forward it unmodified ({{MOQT}}). A Relay can therefore
identify data by Track Alias on any session where the extension is negotiated,
regardless of whether it was negotiated on the upstream session. When a Relay
forwards data received on a session without the extension to a session with
it, it MAY replace the Request ID with the Track Alias. When it forwards data
identified by Track Alias to a session without the extension, it MUST replace
the Track Alias with the Request ID of the downstream subscription.

# Error Handling {#errors}

DUPLICATE_TRACK_ALIAS (0x5):
: A session termination error code indicating that the peer sent a TRACK_ALIAS
  already in use by an `Established` subscription to a different Track
  ({{using}}).

# Security Considerations

A TRACK_ALIAS is the same across sessions, so an observer of decrypted data on
several sessions can correlate them by Track. This is no more than the Full
Track Name already reveals to such an observer.

Data identified by a TRACK_ALIAS that is never established consumes buffer space
at the subscriber, as with data for an unknown Request ID in {{MOQT}}.
Subscribers SHOULD bound the data they buffer for unknown identifiers.

# IANA Considerations

This document registers entries in registries established by {{MOQT}}. All
codepoints are provisional pending working group adoption and can be reassigned
by IANA to avoid collisions.

IANA is requested to add the following entry to the "MOQT Setup Options"
registry:

| Type | Name | Specification |
|-----:|:-----|:--------------|
| 0x0D | TRACK_ALIAS_DATA | {{negotiation}} |

IANA is requested to add the following entry to the "MOQT Session Termination
Error Codes" registry:

| Name | Code | Specification |
|:-----|:----:|:--------------|
| DUPLICATE_TRACK_ALIAS | 0x5 | {{errors}} |

--- back

# Acknowledgments
{:numbered="false"}

This draft was written with the assistance of Claude Code.
