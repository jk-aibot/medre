# Promote MeshCore session teardown and Chatmail retirement qualification

Promote the MeshCore adapter whose session stop clears the inbound callback
before its first await, so no SDK event dispatched during teardown reaches a
retired callback, and whose start refuses while an earlier start's session
remains installed, so a cancelled startup's partial session always retires
through `stop()`, including the BLE stale-link release. The MeshCore transport
profile describes both boundaries.

Promote the Chatmail adapter whose SDK-tier suite qualifies RPC retirement and
native profile exclusion against the pinned client and server: pending calls
fail once the native process dies, shutdown reaps the process before releasing
the profile lease, the native account lock excludes a second manager until
process death, and interpreter exit stays unblocked. Chatmail runtime behavior
is unchanged.
