# Audit: GNA (GLP Networking API) against the GLP catalogue (appendix-guards.tex)

A = /home/claude/gna/sections/*.tex (introduction, api, proximity, ip, system-predicates, rendezvous, directory, summary, implementation-notes) and main.tex.
B = /mnt/user-data/uploads/Grassroots/GLP-Spec/sections/appendix-guards.tex.
Line numbers are physical lines. Most of B's networking text is on the long lines 300-325.

## Missing constructs

1. **`Presence` and `Reach` are not in B's list of predefined types.**
   GNA system-predicates.tex:5: "reachable(Events), the last a stream of connected(Key) and lost(Key)".
   B:6: "PlaceEvent, Token, ClockStep, Compiled" (no `Presence` or `Reach`). B:310 defines both only inside the `Declaration` paragraph.
   B uses both types in `Declaration` but leaves them out of the predefined-types list, while every other networking type (PeerAddress, App, Declaration, Removal, Underlay, TrustLevel, PlaceEvent) is in it.

2. **Nothing gives a program the agent's own public address or tells it when that address changes.**
   GNA ip.tex:21: "GLP learns the address from onConnectivityStatusChanged/getPublicAddress, sends it to friends".
   B: absent. B:310 `peer_address/2` reports only a peer's address, and B has no stream or predicate for the agent's own address.
   GNA says GLP reads the agent's own address and its changes and passes them to friends, and B gives a program no way to do that.

3. **Nothing gives a program the local network fingerprint or tells it when it changes.**
   GNA cold-call / trust-levels, api.tex:169: "LAN contact while it is attached to a local network the person declared trusted". See also ip.tex:50, 63-65 (`networkIdentity`, `onNetworkChanged`).
   B: absent. B:323-325 explains proximity trust only through places.
   GNA expects GLP to raise LAN trust on a network the person declared trusted, but B has no predicate or stream that tells a program which local network it is attached to.

4. **Nothing turns link text back into a signed term.**
   GNA rendezvous.tex:47: "the inviter's person sends the link, as text, over any channel they have". Also directory.tex:21: "the link is given as text, to open in a Grassroots App".
   B:204: "procedure term_to_string(_?, String)." B has no inverse (parse or string-to-term).
   The recipient's agent has to verify and redeem a link it received as text, but B offers no construct that rebuilds a `SignedTerm` from a string.

5. **A program cannot see per-underlay reachability over PAN or LAN.**
   GNA api.tex:55: "GLP computes which of its friends are physically nearby by intersecting ... reachable over PAN".
   B:316 and B:318: `nearby` reports discovery (`seen`/`gone`), and `reachable` reports "over the WAN" only.
   GNA says GLP sees which underlays a peer is reachable over (`onPeerConnected`/`peerUnderlays` on PAN and LAN), but B exposes connection reachability only for the WAN.

6. **No seam reaches the directory's mail server or web page** (low; GNA may intend these to stay outside GLP).
   GNA directory.tex:28: "with a web server for its page and a mail server for its verification messages".
   B: absent.
   The directory agent sends verification mail and answers lookups from page clicks (directory.tex:20, 25), and B has no seam predicate to a mail or web server. GNA calls these "by hand" implementation pragmas (directory.tex:5), so the gap may be intentional.

## Mismatches

7. **`Underlay` names different things in the two papers.**
   GNA implementation-notes.tex:13: "Underlay with the values pan, lan and wan, ProximityUnderlay with pan and lan".
   B:310: "Underlay ::= pan ; lan".
   B uses the name `Underlay` for what GNA calls `ProximityUnderlay`. GNA's `Underlay` also includes `wan`.

8. **`sign/3` takes a key argument, but the layer signs only under the agent's own key.**
   GNA system-predicates.tex:28: "Ed25519 signing and verification under the agent's key and against a public key". Also impl:58: "key pair is private to the layer, which ... signs by sign".
   B:300: "requires Term ground and Key a key of that person".
   GNA's layer has exactly one signing key, the agent's, while B's `Key` argument allows other keys and does not say what happens when `Key` is not `self_key`.

9. **B does not say which module identity a signature carries.**
   GNA system-predicates.tex:28: "adding the source identity of the signing program". Also rendezvous.tex:50: "changes the source identity a signed term carries".
   B:300: "the pair of Term and the identity of the module making the call".
   GNA fixes the signed identity as the source identity. B says only "the identity of the module", although B:285-287 separates source identity from compiled identity.

10. **`remove(peer(P))` also ends P's live sessions, which B does not say.**
    GNA api.tex:78: "removing a key ... ends the peer's live sessions on every underlay".
    B:312: "takes P, and any address recorded for it, off the layer's known peers".
    B leaves out that the removal ends the peer's sessions on every underlay. A program sees the consequences: `lost`/`gone` events, and messages returned to the queue (impl:58).

11. **Declaring a peer is a precondition for WAN contact, and B states it nowhere.**
    GNA api.tex:131: "the layer connects over the WAN only to known peers". Also api.tex:172 and ip.tex:73: "whose programs have each declared the other's key to their layer".
    B:312: "gives the networking layer the public key P of a peer the program knows". B:282 `send_to_net` places no such condition.
    B does not say that `peer(P)` is what Closed trust recognises and what WAN contact needs, so `send_to_net` to an undeclared key never connects over the WAN.

12. **B says "in order" where GNA says delivery is unordered.**
    GNA api.tex:215: "Messages between two agents may be delivered in any order".
    B:282: "sends each element of Stream ... to agent Q, in order".
    B's "in order" can be read as ordered delivery. GNA guarantees only fair, unordered delivery, queued across unreachability and termination.

13. **`address(P, A)` also makes P a known peer, and a later observed address replaces A.**
    GNA impl:33: "creates the peer's entry even for a peer never seen ... joins the known-peer set". Also ip.tex:38: "the latest, whether GLP supplied it or the layer observed it, replaces".
    B:312: "address(P, A) gives the layer the address A at which peer P is reached".
    B does not say that declaring an address makes P a known peer (recognised under Closed trust and admitted over the WAN), or that a later address the layer observes overrides the one the program declared.

14. **Open trust means initiating contact, not only answering it.**
    GNA proximity.tex:18: "under Open the agent contacts or answers unmatched presences on that underlay".
    B:323: "decides whether the agent answers an unsolicited approach from a device it does not already know".
    GNA's Open level makes the agent initiate contact with strangers and reveal its key in ANNOUNCE. B describes answering only.

15. **`gone(K)` has a different meaning.**
    GNA proximity.tex:35: "its presence is no longer observed and it holds no session on the underlay".
    B:316: "gone(K) when that agent can no longer be reached over U".
    GNA's loss needs both the presence gone and no session. B's "can no longer be reached" is a different and looser condition.

16. **`connected(K)` has a different meaning and covers more agents.**
    GNA api.tex:131: "once its session ... is established and authenticated, and the attestation exchange ... has completed". Also impl:58: rendezvous server sessions "reported reachable, unattested".
    B:318: "connected(K) when the layer has a session with the agent of key K over the WAN".
    GNA reports a peer only after attestation completes. Declared rendezvous servers also appear on this stream. B says neither.

17. **The place centre is fixed at first declaration, not at each call.**
    GNA api.tex:152: "the centre is the device's location when the agent first declares the place". The runtime keeps it and gives it again at a restart.
    B:314: "centred on the declaring agent's location at the time of the call".
    After a restart, GNA reuses the original centre, while B implies the place is re-centred wherever the device is then.

18. **The papers disagree on who holds the private key** (low: not visible to a program).
    GNA api.tex:15: "The layer holds the private key, signs with it and authenticates the sender".
    B:300: "The runtime makes the agent's key pair ... and holds it".
    GNA makes the key pair private to the layer (impl:58, decision 39), while B says the runtime holds it.

## Edge cases

19. **A place declared while reporting is stopped is told so at once.**
    GNA api.tex:154: "a place declared while reporting is stopped is told so as soon as it is declared".
    B:314: absent.
    In GNA such a stream begins with `unobservable`. B does not say so. B also omits that on iOS the device is `unobservable` whenever the app is not in the foreground.

20. **A headless agent refuses place declarations.**
    GNA api.tex:154: "A headless server has no location service ... refuses declarePlace and removePlace".
    B:314: absent.
    A rendezvous or directory agent that calls `declare(place(...))` or `remove(place(...))` gets something B never states: failure, an abort or a no-op.

21. **B says nothing about calls on an underlay the layer does not run.**
    GNA api.tex:9: "an unimplemented underlay is simply absent from discovery and peerUnderlays". Also api.tex:48: "finds no sub-object", and impl:13: headless "has no trust level".
    B:310-318: absent.
    B does not say what `declare(trust(pan, _))`, `nearby(lan, _)`, `punch_udp/1`, `peer_address/2` or `rendezvous(...)` do on an agent without that underlay.

22. **The radius unit and the rejection cases are missing.**
    GNA api.tex:152: "a circle of a given radius in metres". Also impl:94: "A radius that is not a positive, finite number of metres is rejected".
    B:314: "declares a place P of radius R".
    B gives no unit and no outcome for an invalid radius, or for a platform refusal, after which "the place is left undeclared" (impl:94, platform geofence cap).

23. **The `peer_address/2` details are missing.**
    GNA impl:58: "reports the address observed on the live WAN session, else on the live LAN session". Also ip.tex:40: "public ip:port".
    B:310: "S the address at which the networking layer observes peer P".
    B does not say that `S` is an `ip:port` string read from a live session only (never the recorded address), or that it falls back to a LAN, non-public address.

24. **B does not say what `self_app/2` gives when the layer attests nothing.**
    GNA api.tex:146: "A headless server profile has no attestation to offer". Also impl:71: a non-integer CFBundleVersion "gives no attestation".
    B:310: "where the runtime is given no app, as in a simulation, each is none".
    B covers only the simulation. It does not say what `R` is on a headless server or on a platform without attestation, where peers see `unattested`.

25. **B does not say a signed term is ground.**
    GNA rendezvous.tex:47: "signed with its own key, a signed term being ground".
    B:300: absent.
    GNA relies on a `SignedTerm` being ground, so it can be sent and matched. B states this nowhere.

26. **B does not fix how a `Key` is encoded as a string, so key order may not match the layer's.**
    GNA rendezvous.tex:44: "PkA the lexicographically smaller key". Also proximity.tex:15: the layer's initiator is by "lexicographically smaller public key".
    B:8 and B:41: a key is a string, and strings compare by character codes.
    `@<` on keys agrees with the layer's byte order only for an order-preserving encoding such as lowercase hex, and B does not fix the encoding.

27. **Re-declaring a server's address keeps its session.**
    GNA impl:85: "A declaration of a rendezvous server whose address changes keeps a standing session with it".
    B:312: "or replaces its address".
    B does not say the session survives an address replacement, so `reachable` reports no `lost` for it.

28. **Under Open PAN trust, a known peer whose iOS app is in the background is not seen** (implementation deviation, open item).
    GNA impl:108: "Under Open PAN trust the scan is by the prefix alone".
    B:316: "seen(K) when the layer discovers on U an agent of key K that it recognises".
    While this deviation stands, raising PAN trust to Open hides recognised peers whose iOS app is in the background, and B does not say so.

29. **The trust level may persist across a restart** (low; it depends on whether the layer restores the persisted level).
    GNA impl:39: "The persisted settings carry a trust level per proximity underlay".
    B:323: "Both underlays stand at closed until declared".
    If the layer restores a persisted level, an agent can stand at Open after a restart without declaring it, contrary to B.

## Categories with nothing to report

- Answer types: GNA introduces none that a program gets from the layer. The `Reply` values of the rendezvous and directory protocols (`punch(Key, Address)`, `verify`, `rejected`, `listed`, `unlisted`, `more(N)`, `supply(A, Links)`) belong to those programs, not to the layer, so they do not belong in B.
- Application protocol terms (`invitation/5`, `register/3`, `redeem/3`, `attest/2`, `list/4`, `unlist/3`, `listing/4`): these are GLP programs' own messages, not catalogue constructs. No finding.
- Not visible to a program and not counted:
  - GNA calls the seam "five system predicates" and does not list `self_app/2`, which B places on the platform side.
  - GNA puts the predicates' clauses in "the implementation paper" (system-predicates.tex:5), while B puts them in `programs/self.glp` (B:310).
  - GNA impl:122 records an open proposal for a seam stream reporting observed peer addresses. It is undecided, so it is not counted.

Checked and agreeing: `peer_address/2` and `PeerAddress ::= address(String) ; none`; `peer_app/2` and `App ::= app(String, String, Integer) ; unattested ; none` (developer, name, version; null maps to `unattested`); rendezvous server reported with no app (`unattested`); `self_app/2` version being the one the runtime gives the layer, the earlier one after a refused update; `punch_udp/1` (assigns nothing, carries no payload); `declare/1` alternatives `peer/1`, `address/2`, `rendezvous/2`, `trust/2`, `place/3`, `nearby/2`, `reachable/1` with their arities; `remove/1` alternatives `peer/1`, `rendezvous/1`, `place/1`, `nearby/1`, `reachable/0`; `TrustLevel ::= open ; closed`; trust defaulting to closed per underlay, set independently, a later declaration replacing; `PlaceEvent ::= entered ; exited ; observable ; unobservable`; crossings lost while unobservable; place supersession; `remove(place)` and `remove(rendezvous)` of an undeclared name doing nothing; rendezvous re-declaration replacing the address; `remove(rendezvous)` ending the session; `Reach` alternatives `connected/1` and `lost/1` over the WAN; `Presence` alternatives `seen/1` and `gone/1`, with `seen` for recognised agents or, under Open trust, contacted ones; `self_key/1` = `getIdentity`; `signature/2` over `verify`; `Signature ::= signed(Key, Hash, _) ; unsigned`; `NetMsg ::= msg(Key, X)` and the cold call to the index-0 serializer (`'_w'(Q, 0, 0)`); `send_to_net/1` over `send`; `now/1` in milliseconds as the unit of link expiry.
