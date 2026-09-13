# Sentence diff: `74a8e45537~1` → `HEAD`

| | |
|---|---:|
| old units | 2377 |
| new units | 2379 |
| unchanged | 2343 (98.5% of new) |
| modified | 15 |
| added | 21 |
| removed | 19 |
| **total findings** | **55** |

_Section references and anchors are normalized to `§`, so retargeting a reference is not reported. Pass `--keep-refs` to include them._

## Modified (15)

`Relays > Publisher Interactions` · 98% similar · L2158

> Namespace Prefix Matching **(§)** is further used to decide which publishers receive a
> SUBSCRIBE and which subscribers receive a PUBLISH.

`Publisher and Namespace Discovery > Subscribing to Namespaces > Namespace Subscription Authorization` ← `Control Messages > SUBSCRIBE_TRACKS` · 97% similar · L1314

> The publisher MUST ensure the subscriber is authorized to perform ~~this~~ **a**
> namespace subscription.

`Publisher and Namespace Discovery > Publishing Namespaces` ← `Namespace Discovery > Publishing Namespaces` · 96% similar · L1241

> A PUBLISH_NAMESPACE is withdrawn by cancelling the request (see §), although it is not a
> protocol error for the subscriber to send a ~~SUBSCRIBE~~ **SUBSCRIBE, FETCH** or
> ~~FETCH~~ **TRACK_STATUS** message for a track in a namespace after the namespace is
> withdrawn.

`Publisher and Namespace Discovery > Publishing Namespaces` ← `Namespace Discovery > Publishing Namespaces` · 95% similar · L1236

> If ~~it~~ **a subscriber** has accepted a PUBLISH_NAMESPACE with a namespace that
> exactly matches the namespace for ~~that~~ **a given** track, it SHOULD only request it
> from the senders of those PUBLISH_NAMESPACE messages.

`Publisher and Namespace Discovery > Subscribing to Namespaces` ← `Namespace Discovery > Subscribing to Namespaces` · 93% similar · L1259

> If the subscriber is aware of a namespace of interest, it can send SUBSCRIBE_NAMESPACE
> ~~or SUBSCRIBE_TRACKS~~ to publishers/relays it has established a session with.

`Publisher and Namespace Discovery > Subscribing to Namespaces` ← `Namespace Discovery > Subscribing to Namespaces` · 92% similar · L1259

> The Track Namespace Prefix ~~carried in these messages~~ **it carries** is compared
> against the namespaces known to the receiver using Namespace Prefix Matching (§).

`Publisher and Namespace Discovery > Publishing Namespaces` ← `Namespace Discovery > Publishing Namespaces` · 92% similar · L1216

> A subscriber MAY send ~~SUBSCRIBE~~ **SUBSCRIBE, FETCH** or ~~FETCH~~ **TRACK_STATUS**
> for tracks in a namespace without having received a PUBLISH_NAMESPACE for it.

`Publisher and Namespace Discovery > Subscribing to Namespaces` ← `Namespace Discovery > Subscribing to Namespaces` · 91% similar · L1309

> A SUBSCRIBE_NAMESPACE ~~or SUBSCRIBE_TRACKS~~ is cancelled as described in §, by
> resetting or sending STOP_SENDING on the stream.

`Publisher and Namespace Discovery` ← `Namespace Discovery` · 87% similar · L1204

> Given sufficient ~~out of band~~ **out-of-band** information, it is valid for a
> subscriber to ~~send a SUBSCRIBE or FETCH message to~~ **retrieve tracks from** a
> publisher (including a relay) without any previous MOQT messages besides SETUP.

`Publisher and Namespace Discovery > Subscribing to Namespaces` ← `Namespace Discovery > Subscribing to Namespaces` · 86% similar · L1288

> The ~~receiver of a REQUEST_OK or REQUEST_ERROR~~ **subscriber** ought to forward the
> result to the application, so the application can decide which other publishers to
> contact, if any.

`Publisher and Namespace Discovery > Subscribing to Namespaces` ← `Control Messages > SUBSCRIBE_NAMESPACE` · 84% similar · L1277

> ~~If it is an~~ **On** error, the stream ~~will be~~ **is** immediately closed via FIN.

`Control Messages > SUBSCRIBE_NAMESPACE` ← `Control Messages > SUBSCRIBE_TRACKS` · 83% similar · L3569

> Track Namespace Prefix: A Track Namespace structure as described in ~~§.~~ **§, matched
> as a prefix (see §).**

`Introduction > Document Structure` · 82% similar · L95

> Section 4 § Describes mechanisms for discovering **Publishers and** Namespaces ~~and
> Tracks~~

`Publisher and Namespace Discovery > Subscribing to Namespaces` ← `Namespace Discovery > Subscribing to Namespaces` · 78% similar · L1268

> ~~Either message~~ **A SUBSCRIBE_NAMESPACE** with zero Track Namespace fields indicates
> the sender is interested in all namespaces ~~or all tracks~~ from the ~~receiver,
> respectively.~~ **receiver.**

`Publisher and Namespace Discovery > Subscribing to Namespaces` ← `Control Messages > NAMESPACE_DONE` · 71% similar · L1284

> ~~The~~ **A NAMESPACE_DONE indicates the** publisher ~~sends the NAMESPACE_DONE control
> message to indicate its intent~~ **intends** to stop serving new subscriptions for
> tracks within ~~the provided Track Namespace.~~ **that namespace.**

## Added (21)

`Object Data Model > Track > Namespace Prefix Matching` · L503

> **To perform a namespace prefix match, the fields of the prefix are compared
> sequentially against the leading fields of the Track Namespace or Full Track Name being
> matched, requiring an exact match for each field.**

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

`Publishing and Receiving Tracks > Subscribing to Tracks by Prefix` · L1102

> **A SUBSCRIBE_TRACKS with zero Track Namespace fields indicates the sender is interested
> in all tracks from the receiver.**

`Publishing and Receiving Tracks > Subscribing to Tracks by Prefix` · L1127

> **A SUBSCRIBE_TRACKS is cancelled as described in §, by resetting or sending
> STOP_SENDING on the stream.**

`Publisher and Namespace Discovery` · L1204

> **However, MOQT provides in-band messages for a publisher to advertise the namespaces it
> has tracks in, and for a subscriber to enumerate the namespaces a publisher knows.**

`Publisher and Namespace Discovery` · L1210

> **Discovery of MOQT servers is always done out-of-band: MOQT does not specify how an
> endpoint learns where to establish a session.**

`Publisher and Namespace Discovery` · L1210

> **The discovery described in this section takes place within an established session.**

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

`Publisher and Namespace Discovery > Namespace Discovery Example` · L1334

> **In the following example, a subscriber asks a relay for namespaces under a prefix, a
> publisher subsequently advertises a matching namespace to that relay, and the relay
> passes it on.**

`Publisher and Namespace Discovery > Namespace Discovery Example` · L1334

> **When the publisher withdraws its advertisement, the relay tells the subscriber the
> namespace is gone.**

`Publisher and Namespace Discovery > Namespace Discovery Example` · L1361

> **The NAMESPACE and NAMESPACE_DONE messages carry only the suffix 123, because the
> prefix example is already known from the SUBSCRIBE_NAMESPACE.**

`Control Messages > NAMESPACE_DONE` · L3600

> **The publisher sends the NAMESPACE_DONE control message on the response stream of a
> SUBSCRIBE_NAMESPACE request.**

## Removed (19)

`Namespace Discovery` · L1120

> ~~Discovery of MOQT servers is always done out-of-band.~~

`Namespace Discovery` · L1120

> ~~Namespace discovery can be done in the context of an established MOQT session using
> SUBSCRIBE_NAMESPACE (see §).~~

`Namespace Discovery` · L1124

> ~~However, SUBSCRIBE_NAMESPACE, SUBSCRIBE_TRACKS, PUBLISH and PUBLISH_NAMESPACE messages
> provide an in-band means of discovery of publishers for a namespace.~~

`Namespace Discovery` · L1130

> ~~The syntax of these messages is described in §.~~

`Namespace Discovery > Subscribing to Namespaces` · L1141

> ~~SUBSCRIBE_NAMESPACE requests namespace discovery: the publisher sends relevant
> NAMESPACE and NAMESPACE_DONE messages for namespaces matching the prefix, including
> echoing back Track Namespaces under the prefix that have been published to it.~~

`Namespace Discovery > Subscribing to Namespaces` · L1158

> ~~The subscriber sends SUBSCRIBE_NAMESPACE or SUBSCRIBE_TRACKS on a new bidirectional
> stream and the publisher MUST send a single REQUEST_OK or REQUEST_ERROR as the first
> message on the bidirectional stream in response.~~

`Namespace Discovery > Publishing Namespaces` · L1192

> ~~If a publisher is the Original Publisher for one or more tracks in a given namespace,
> or is a relay that has received an authorized PUBLISH_NAMESPACE for that namespace from
> an upstream publisher, it MUST send a NAMESPACE message that includes this namespace to
> any subscriber that has sent a SUBSCRIBE_NAMESPACE whose prefix matches this
> namespace.~~

`Namespace Discovery > Publishing Namespaces` · L1230

> ~~A subscriber MAY send a SUBSCRIBE or FETCH for a track to any publisher.~~

`Relays > Publisher Interactions` · L2036

> ~~In this process, the fields in the Track Namespace are matched sequentially, requiring
> an exact match for each field.~~

`Relays > Publisher Interactions` · L2036

> ~~If the published or subscribed Track Namespace has the same or fewer fields than the
> Track Namespace in the message, it qualifies as a match.~~

`Relays > Publisher Interactions` · L2043

> ~~For example: A SUBSCRIBE message with namespace=(foo, bar) and name=x will match
> sessions that sent PUBLISH_NAMESPACE messages with namespace=(foo) or namespace=(foo,
> bar).~~

`Relays > Publisher Interactions` · L2043

> ~~It will not match a session with namespace=(foobar).~~

`Control Messages > SUBSCRIBE_TRACKS` · L3566

> ~~This prefix is matched against track namespaces known to the publisher.~~

`Control Messages > SUBSCRIBE_NAMESPACE` · L3457

> ~~For example, using the serialized format from §, if the publisher is a relay that has
> received PUBLISH_NAMESPACE messages for namespaces example.2ecom-123-100 and
> example.2ecom-123-200, a SUBSCRIBE_NAMESPACE for example.2ecom-123 would match both.~~

`Control Messages > SUBSCRIBE_NAMESPACE` · L3468

> ~~The publisher will respond with SUBSCRIBE_NAMESPACE_OK or SUBSCRIBE_NAMESPACE_ERROR on
> the response half of the stream.~~

`Control Messages > SUBSCRIBE_NAMESPACE` · L3468

> ~~If the subscriber receives any message other than a SUBSCRIBE_NAMESPACE_OK or a
> SUBSCRIBE_NAMESPACE_ERROR as the first message on the response half of the stream, then
> it MUST close the session with a PROTOCOL_VIOLATION.~~

`Control Messages > SUBSCRIBE_NAMESPACE` · L3468

> ~~If the SUBSCRIBE_NAMESPACE is successful, the publisher will send matching NAMESPACE
> messages on the response stream.~~

`Control Messages > SUBSCRIBE_NAMESPACE` · L3468

> ~~When there are changes to the namespaces being published and the subscriber is
> subscribed to them, the publisher sends the corresponding NAMESPACE or NAMESPACE_DONE
> messages.~~

`Control Messages > NAMESPACE` · L3502

> ~~The Track Namespace Prefix from the SUBSCRIBE_NAMESPACE followed by the Track
> Namespace Suffix is the Track Namespace Prefix the publisher advertised, so tracks can
> exist in namespaces matching that prefix (see §).~~
