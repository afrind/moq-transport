# Sentence diff: `HEAD~1` → `HEAD`

| | |
|---|---:|
| old units | 2378 |
| new units | 2376 |
| unchanged | 2355 (99.1% of new) |
| modified | 9 |
| added | 12 |
| removed | 14 |
| **total findings** | **35** |

_Section references and anchors are normalized to `§`, so retargeting a reference is not reported. Pass `--keep-refs` to include them._

## Modified (9)

`Publisher and Namespace Discovery > Subscribing to Namespaces > Namespace Subscription Authorization` ← `Publisher and Namespace Discovery > Subscribing to Namespaces` · 97% similar · L1314

> The publisher MUST ensure the subscriber is authorized to perform ~~this~~ **a**
> namespace subscription.

`Publisher and Namespace Discovery > Publishing Namespaces` · 96% similar · L1241

> A PUBLISH_NAMESPACE is withdrawn by cancelling the request (see §), although it is not a
> protocol error for the subscriber to send a ~~SUBSCRIBE~~ **SUBSCRIBE, FETCH** or
> ~~FETCH~~ **TRACK_STATUS** message for a track in a namespace after the namespace is
> withdrawn.

`Publisher and Namespace Discovery > Publishing Namespaces` · 95% similar · L1236

> If ~~it~~ **a subscriber** has accepted a PUBLISH_NAMESPACE with a namespace that
> exactly matches the namespace for ~~that~~ **a given** track, it SHOULD only request it
> from the senders of those PUBLISH_NAMESPACE messages.

`Publisher and Namespace Discovery > Publishing Namespaces` · 92% similar · L1216

> A subscriber MAY send ~~SUBSCRIBE~~ **SUBSCRIBE, FETCH** or ~~FETCH~~ **TRACK_STATUS**
> for tracks in a namespace without having received a PUBLISH_NAMESPACE for it.

`Publisher and Namespace Discovery > Subscribing to Namespaces` · 86% similar · L1288

> The ~~receiver of a REQUEST_OK or REQUEST_ERROR~~ **subscriber** ought to forward the
> result to the application, so the application can decide which other publishers to
> contact, if any.

`Publisher and Namespace Discovery > Subscribing to Namespaces` · 84% similar · L1277

> ~~If it is an~~ **On** error, the stream ~~will be~~ **is** immediately closed via FIN.

`Control Messages > SUBSCRIBE_NAMESPACE` ← `Control Messages > SUBSCRIBE_TRACKS` · 83% similar · L3537

> Track Namespace Prefix: A Track Namespace structure as described in ~~§.~~ **§, matched
> as a prefix (see §).**

`Publisher and Namespace Discovery > Subscribing to Namespaces` ← `Control Messages > NAMESPACE_DONE` · 71% similar · L1284

> ~~The~~ **A NAMESPACE_DONE indicates the** publisher ~~sends the NAMESPACE_DONE control
> message to indicate its intent~~ **intends** to stop serving new subscriptions for
> tracks within ~~the provided Track Namespace.~~ **that namespace.**

`Object Data Model > Track > Namespace Prefix Matching` · 70% similar · L503

> To perform a namespace prefix match, the fields ~~in~~ **of the prefix are compared
> sequentially against the leading fields of** the Track Namespace ~~are matched
> sequentially,~~ **or Full Track Name being matched,** requiring an exact match for each
> field.

## Added (12)

`Object Data Model > Track > Namespace Prefix Matching` · L503

> **The prefix matches if it has the same or fewer fields.**

`Object Data Model > Track > Namespace Prefix Matching` · L508

> **The examples below use the serialized name format from §.**

`Object Data Model > Track > Namespace Prefix Matching` · L511

> **The name foo-bar--x matches the prefixes foo and foo-bar.**

`Object Data Model > Track > Namespace Prefix Matching` · L511

> **It does not match foobar.**

`Object Data Model > Track > Namespace Prefix Matching` · L514

> **The prefix example.2ecom-123 matches the namespaces example.2ecom-123-100 and
> example.2ecom-123-200.**

`Publisher and Namespace Discovery > Subscribing to Namespaces` · L1265

> **SUBSCRIBE_NAMESPACE requests namespace discovery: the publisher responds with
> NAMESPACE and NAMESPACE_DONE messages.**

`Publisher and Namespace Discovery > Subscribing to Namespaces` · L1271

> **The subscriber sends SUBSCRIBE_NAMESPACE on a new bidirectional stream.**

`Publisher and Namespace Discovery > Subscribing to Namespaces` · L1271

> **The publisher MUST send a single SUBSCRIBE_NAMESPACE_OK or SUBSCRIBE_NAMESPACE_ERROR
> as the first message on the response half of the stream; if the subscriber receives any
> other message first, it MUST close the session with a PROTOCOL_VIOLATION.**

`Publisher and Namespace Discovery > Subscribing to Namespaces` · L1277

> **On success, the publisher MUST send a NAMESPACE message for each namespace it knows
> that matches the Track Namespace Prefix, and further NAMESPACE or NAMESPACE_DONE
> messages as that set changes.**

`Publisher and Namespace Discovery > Subscribing to Namespaces` · L1277

> **A publisher knows a namespace if it is the Original Publisher for one or more tracks
> in it, or is a relay that has received an authorized PUBLISH_NAMESPACE for it from an
> upstream publisher.**

`Publisher and Namespace Discovery > Subscribing to Namespaces` · L1284

> **The namespace in a NAMESPACE message is itself a prefix; tracks can exist in
> namespaces matching it.**

`Control Messages > NAMESPACE_DONE` · L3568

> **The publisher sends the NAMESPACE_DONE control message on the response stream of a
> SUBSCRIBE_NAMESPACE request.**

## Removed (14)

`Object Data Model > Track > Namespace Prefix Matching` · L503

> ~~If the published or subscribed Track Namespace has the same or fewer fields than the
> Track Namespace in the message, it qualifies as a match.~~

`Object Data Model > Track > Namespace Prefix Matching` · L508

> ~~For example: A SUBSCRIBE message with namespace=(foo, bar) and name=x will match
> sessions that sent PUBLISH_NAMESPACE messages with namespace=(foo) or namespace=(foo,
> bar).~~

`Object Data Model > Track > Namespace Prefix Matching` · L508

> ~~It will not match a session with namespace=(foobar).~~

`Publisher and Namespace Discovery > Publishing Namespaces` · L1227

> ~~If a publisher is the Original Publisher for one or more tracks in a given namespace,
> or is a relay that has received an authorized PUBLISH_NAMESPACE for that namespace from
> an upstream publisher, it MUST send a NAMESPACE message that includes this namespace to
> any subscriber that has sent a SUBSCRIBE_NAMESPACE whose prefix matches this
> namespace.~~

`Publisher and Namespace Discovery > Publishing Namespaces` · L1260

> ~~A subscriber MAY send a SUBSCRIBE or FETCH for a track to any publisher.~~

`Publisher and Namespace Discovery > Subscribing to Namespaces` · L1273

> ~~SUBSCRIBE_NAMESPACE requests namespace discovery: the publisher sends relevant
> NAMESPACE and NAMESPACE_DONE messages for namespaces matching the prefix, including
> echoing back Track Namespaces under the prefix that have been published to it.~~

`Publisher and Namespace Discovery > Subscribing to Namespaces` · L1286

> ~~The subscriber sends SUBSCRIBE_NAMESPACE on a new bidirectional stream and the
> publisher MUST send a single REQUEST_OK or REQUEST_ERROR as the first message on the
> bidirectional stream in response.~~

`Publisher and Namespace Discovery > Subscribing to Namespaces` · L1294

> ~~The publisher will respond with SUBSCRIBE_NAMESPACE_OK or SUBSCRIBE_NAMESPACE_ERROR on
> the response half of the stream.~~

`Publisher and Namespace Discovery > Subscribing to Namespaces` · L1294

> ~~If the subscriber receives any message other than a SUBSCRIBE_NAMESPACE_OK or a
> SUBSCRIBE_NAMESPACE_ERROR as the first message on the response half of the stream, then
> it MUST close the session with a PROTOCOL_VIOLATION.~~

`Publisher and Namespace Discovery > Subscribing to Namespaces` · L1294

> ~~If the SUBSCRIBE_NAMESPACE is successful, the publisher will send matching NAMESPACE
> messages on the response stream.~~

`Publisher and Namespace Discovery > Subscribing to Namespaces` · L1294

> ~~When there are changes to the namespaces being published and the subscriber is
> subscribed to them, the publisher sends the corresponding NAMESPACE or NAMESPACE_DONE
> messages.~~

`Control Messages > SUBSCRIBE_TRACKS` · L3613

> ~~This prefix is matched against track namespaces known to the publisher.~~

`Control Messages > SUBSCRIBE_NAMESPACE` · L3536

> ~~For example, using the serialized format from §, if the publisher is a relay that has
> received PUBLISH_NAMESPACE messages for namespaces example.2ecom-123-100 and
> example.2ecom-123-200, a SUBSCRIBE_NAMESPACE for example.2ecom-123 would match both.~~

`Control Messages > NAMESPACE` · L3549

> ~~The Track Namespace Prefix from the SUBSCRIBE_NAMESPACE followed by the Track
> Namespace Suffix is the Track Namespace Prefix the publisher advertised, so tracks can
> exist in namespaces matching that prefix (see §).~~
