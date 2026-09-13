# Sentence diff: `HEAD~1` → `HEAD`

| | |
|---|---:|
| old units | 2377 |
| new units | 2379 |
| unchanged | 2372 (99.7% of new) |
| modified | 5 |
| added | 2 |
| removed | 0 |
| **total findings** | **7** |

_Section references and anchors are normalized to `§`, so retargeting a reference is not reported. Pass `--keep-refs` to include them._

## Modified (5)

`Namespace Discovery > Subscribing to Namespaces` · 95% similar · L1234

> The subscriber sends SUBSCRIBE_NAMESPACE ~~or SUBSCRIBE_TRACKS~~ on a new bidirectional
> stream and the publisher MUST send a single REQUEST_OK or REQUEST_ERROR as the first
> message on the bidirectional stream in response.

`Namespace Discovery > Subscribing to Namespaces` · 93% similar · L1215

> If the subscriber is aware of a namespace of interest, it can send SUBSCRIBE_NAMESPACE
> ~~or SUBSCRIBE_TRACKS~~ to publishers/relays it has established a session with.

`Namespace Discovery > Subscribing to Namespaces` · 92% similar · L1215

> The Track Namespace Prefix ~~carried in these messages~~ **it carries** is compared
> against the namespaces known to the receiver using Namespace Prefix Matching (§).

`Namespace Discovery > Subscribing to Namespaces` · 91% similar · L1266

> A SUBSCRIBE_NAMESPACE ~~or SUBSCRIBE_TRACKS~~ is cancelled as described in §, by
> resetting or sending STOP_SENDING on the stream.

`Namespace Discovery > Subscribing to Namespaces` · 78% similar · L1226

> ~~Either message~~ **A SUBSCRIBE_NAMESPACE** with zero Track Namespace fields indicates
> the sender is interested in all namespaces ~~or all tracks~~ from the ~~receiver,
> respectively.~~ **receiver.**

## Added (2)

`Publishing and Receiving Tracks > Subscribing to Tracks by Prefix` · L1098

> **A SUBSCRIBE_TRACKS with zero Track Namespace fields indicates the sender is interested
> in all tracks from the receiver.**

`Publishing and Receiving Tracks > Subscribing to Tracks by Prefix` · L1123

> **A SUBSCRIBE_TRACKS is cancelled as described in §, by resetting or sending
> STOP_SENDING on the stream.**
