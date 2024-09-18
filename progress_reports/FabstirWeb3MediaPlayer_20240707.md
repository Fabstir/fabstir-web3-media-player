## Fabstir Media Player #2 - Progress Report #3

### What progress was made on your grant this month?

- Added support for automatically transferring encryption keys between users; for example, when a user has bought an NFT that contains encrypted video(s).
- Added code for account abstraction tokens (non-transferable NFTs). Will allow users to sign agreements (e.g. legal documents) onchain for use of data, or for token gating, or for certificates.
- Added multi-storage support for media. For example, a video NFT can have its media transcoded to Sia storage (through S5) for smoother playback at higher resolution whilst maintain maximum NFT marketplace compatibility by transcoding a trailer or audio sample to IPFS to allow potential buyers on marketplaces to review before buying. See video demonstration here: https://www.dropbox.com/scl/fi/lrtep4lx9mpzkor87ay0j/Fabstir-Media-Player-minting-video-NFT-20240707p1.mp4
- Started some initial work on the cloud node deployment of the media player.The application software stack consists of maintaining four servers.

### Summarize any problems that you ran into this month and how you'll be solving them.

- Fabstir's decentralised licensing server system is moderately complex. Will need more testing for potential security concerns and/or third party review.
- S5 specs are being finalised so not able to start on adding graph database support to Sia yet.

### Links to repos worked on this month:

https://github.com/Fabstir/Fabstir_Media_Player_Snaps
https://github.com/Fabstir/fabstirdb-backend
https://github.com/Fabstir/fabstirdb
https://github.com/Fabstir/fabstir-transcoder

### What will you be working on next?

- Continue testing of the media player software stack on cloud instances.
- Further integration of the media player with Fabstir's short film platform.
- Implementation of UI for the user account dashboard for transcoding, storage (Sia/S5) and NFT minting fees etc.
