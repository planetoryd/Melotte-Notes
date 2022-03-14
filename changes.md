# Necessary changes

Js-ipfs needs to be forked

- IPFS doesn't respect protocol characteristic issue (though not its fault)
  - TLS self-sgined transport
  - or use existing Wss transport
- Content aware storage and block exchange
  - Melotte data could be versioned, so there's relations between data. Delta-codec etc.
  - Fork bitswap, 
    - Use Melotte-bitswap for melotte peers, Bitswap for usual peers
  - Fork ipfs-repo or create content-aware-store, or fork js-ipfs
    - ipfs-core-config only creates the repo
    - ipfs-repo can access both datastore and blockstore
    - datastore can pass configurations
    - ipfs-repo can wrap the get/put methods
    - Wrapping ipfs-repo in js-ipfs avoids changing ipfs-repo or stores
  - This is more of an IPFS issue. They want git to work on it anyway