## Fabstir Media Player #2 - Progress Report #2

### What progress was made on your grant this month?

- Added multi-chain support. Media player gallery can now list NFTs from multiple EVM compatible blockchains simultaneously and user can play any of them seamlessly.
- User can connect to any of the whitelisted blockchains directly using the wallet widget UI. Then media player can mint or perform transactions on the connected blockchain. User can switch at any time to another chain in the wallet and carry out operations there. Testing was performed on Base Sepolia and Polygon Amoy.
- Added user accounts that are saved to FabstirDB to enable use of the media player without needing MetaMask, and for the user dashboard.

### Summarize any problems that you ran into this month and how you'll be solving them.

- Adding multichain support to the media player greatly increased its functionality, but opened up some  issues for Particle Network wallet to work with this new environment. Had to work with their team and Biconomy to resolve them.
- Waiting on some S5 Rust implementation that will allow for development of FabstirDB database support for Sia.

### Links to repos worked on this month:
https://github.com/Fabstir/Fabstir_Media_Player_Snaps
https://github.com/Fabstir/fabstirdb-backend
https://github.com/Fabstir/fabstirdb
https://github.com/Fabstir/userdb-client-example

### What will you be working on next?
- Implementation of UI for the user account dashboard for transcoding, storage (Sia/S5) and NFT minting fees etc.
- Early testing of the media player on a cloud node
- Add support for graph database to S5/Sia infrastructure