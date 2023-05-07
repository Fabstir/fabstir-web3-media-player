# Fabstir Web3 Media Player - Progress Report (Apr 2023)
By Jules Lai

The production-ready video player that uses a technology stack of Next.js, React, JavaScript/TypeScript and Tailwind is working for local files and media. It features support for multiple playback speeds and subtitles. It also supports songs using .lrc lyric format where the displayed lyrics is able to scroll in sync with the audio.

Progress has also been made to client-side version of S5 Client (called `s5-client.js`) for S5's decentralized content-addressed storage network for storage ultimately on SIA storage. Implemented some fixes to include bearer authentication tokens required by S5, plus contributed some example code. Testing is now ongoing with the Next.js production build of Fabstir Media Player. 


## Past Month Progress

[1]: Base player uses Video.js (https://videojs.com/) as it is an open-source HTML5 video player that plays a range of video formats and subtitles. It also has support for different playback speeds.

[2]: Use Next.js React framework with a mix of server-side and client-side rendering to implement the media player gallery features. This allows for lazy loading of images (of NFTs), only retrieved and rendered as they come into view on the screen. Helps to speed up performance and minimise internet bandwidth required.

[3]: useQuery by TanStack (https://tanstack.com/query/v4/docs/react/reference/useQuery) used to cache queries for data retrieval from SIA Storage and other decentrailsed services. Helps to speed up responses and minimise internet bandwidth required.

[4]: Tested creating NFTs on Hardhat's local network to store NFTs. Able to display gallery of tiles of NFTs and display them with their images and metadata as thumbnails. Plus added a side panel to display larger image and detailed metadata for the currently selected NFT.

[5]: Worked on an example JavaScript browser client-side code to upload and retrieve data to S5 (https://github.com/s5-dev/S5) via s5client.js library (https://github.com/parajbs-dev/s5client-js).

[6]: Created pull-requests merged to `s5client.js` to allow for bearer token authentication for uploads and downloads, plus fixed some issues with metadata retrieval.

[7]: Successfully able to store and retrieve data, NFT metadata and video using `s5client.js` on the browser client-side via JavaScript for the production build environment. Successul test for HLS MPEG-4 AES encryption video streaming, though AV1 codec and XChaCha20 will be the favoured option moving forward for its better compression quality and use of S5's CDN.

## Link to Repos

You'll find these listed in the Fabstir Web3 Media Player repo here https://github.com/Fabstir/fabstir-web3-media-player/blob/main/README.md plus fixes and enhancements here to https://github.com/julesl23/s5client-js

## What I am Working on Next

Test S5's CDN for AV1 encoded video files with XChaCha20 encryption (from SIA storage) for the React and Next.js dapp production ready build.
Test playback of media NFTs on Polygon/Polygon zkEVM testnets with s5 for the media streaming.
Implement the MetaMask local storage of NFT addresses already working on a test player, to the production-ready player to be used as the source to populate a user's media gallery.
Write code that will enable compatibility for media playback for NFTs from exchanges such as OpenSea and Rarible.
There has been some marketing done as well in the form of posts and articles. Included in the road map is the upcoming Cannes Film Festival, where it is hoped to educate filmmakers on content ownership, security/privacy, community involvement and decentralisation.
