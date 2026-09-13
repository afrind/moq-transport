# Sentence diff: `HEAD~1` → `HEAD`

| | |
|---|---:|
| old units | 2379 |
| new units | 2378 |
| unchanged | 2373 (99.8% of new) |
| modified | 2 |
| added | 3 |
| removed | 4 |
| **total findings** | **9** |

_Section references and anchors are normalized to `§`, so retargeting a reference is not reported. Pass `--keep-refs` to include them._

## Modified (2)

`Publisher and Namespace Discovery` ← `Namespace Discovery` · 87% similar · L1200

> Given sufficient ~~out of band~~ **out-of-band** information, it is valid for a
> subscriber to ~~send a SUBSCRIBE or FETCH message to~~ **retrieve tracks from** a
> publisher (including a relay) without any previous MOQT messages besides SETUP.

`Introduction > Document Structure` · 82% similar · L95

> Section 4 § Describes mechanisms for discovering **Publishers and** Namespaces ~~and
> Tracks~~

## Added (3)

`Publisher and Namespace Discovery` · L1200

> **However, MOQT provides in-band messages for a publisher to advertise the namespaces it
> has tracks in, and for a subscriber to enumerate the namespaces a publisher knows.**

`Publisher and Namespace Discovery` · L1206

> **Discovery of MOQT servers is always done out-of-band: MOQT does not specify how an
> endpoint learns where to establish a session.**

`Publisher and Namespace Discovery` · L1206

> **The discovery described in this section takes place within an established session.**

## Removed (4)

`Namespace Discovery` · L1200

> ~~Discovery of MOQT servers is always done out-of-band.~~

`Namespace Discovery` · L1200

> ~~Namespace discovery can be done in the context of an established MOQT session using
> SUBSCRIBE_NAMESPACE (see §).~~

`Namespace Discovery` · L1204

> ~~However, SUBSCRIBE_NAMESPACE, SUBSCRIBE_TRACKS, PUBLISH and PUBLISH_NAMESPACE messages
> provide an in-band means of discovery of publishers for a namespace.~~

`Namespace Discovery` · L1215

> ~~The syntax of these messages is described in §.~~
