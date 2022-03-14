## Arch

![](./arch.drawio.svg)

## Site

The word is derived from ZeroNet. Site is a certain part of IPLD that get synced between its peers together. Site has a management chain, a database, and a codebase. 

## Sync

Sync is done by Pubsub and Bitswap. 

1. After getting updates from Pubsub, the source peer who probably has the blocks is added to Bitswap, so DHT is avoided, similar to ZeroNet in effect.
2. In cases, the peer on Pubsub might not have the blocks, only the CIDs are published on Pubsub. Then the blocks are obtained from known site peers, or via DHT routing, which is less robust.

In practice, a peer subscribes to the site channel on Pubsub when she adds a site. The peers on a site channel may have the latest blocks, outdated blocks, or no blocks. After receiving the notifications from Pubsub, the notifier is supposed to have the latest blocks and added to the routing for Bitswap. If this doesn't succeed, other known peers who are discovered from Pubsub, DHT or other ways are added to Bitswap. If it still fails, DHT is queried with genesis CID, where the result probably represents the all peers available to a site on earth.

Types of peers

- Discoverable peers (not mutually exclusive)
  - Peers from DHT 
  - Directly connected peers
  - Peers connected through anonymity network
-  Distant peers

When a site peer publishes an update, the message is firstly spread among the site peers, and thereafter concurrent syncing begins (CIDs published to Pubsub, source peer added to Bitswap by others if directly connectable, and IPLD sync happens later). 