# Fabstir Web3 Media Player - Progress Report (May 2023)

By Jules Lai

Added support for AV1 encoding to the Fabstir transcoder infrastructure. Tested playback of uploaded transcoded videos to S5 and they stream fine for both HD and 4K resolutions.

Attended the Cannes Film Festival. Met with many professional content creators and facilitators from the film industry, Explained the advantages of Web3, the importance of decentralisation and content ownership. Made many new contacts for Fabstir.

Added support for XChaCha20 encryption of files to `s5client-js`. Allows for files to be automatically encrypted client-side before upload to S5.

## Past Month Progress

### AV1 support added to Fabstir transcoder network

AV1 is a royalty-free modern video codec that is gaining wide-spread support on browsers. It offers much better image quality than the universally supported H264 for the same bandwidth. Browser support includes Chrome, Firefox and Edge. It is a more complex codec than h264 and as such requires much more computation to encode.

My own benchmarks show that a top of the line Intel processor can only transcode at 0.2 fps (frames per second) which is much less than real-time. The same test on Fabstir transcoder network on a top of the range NVIDIA GPU showed transcoding times of over 125 fps for 4K footage (480 fps for HD). This extra speed is due to the 4000 series and Ada Lovelace A6000 GPUs support for hardware encoding of AV1.
Fabstir now uses the AV1 format by default and falls back to H264 for unsupported devices.

### Cannes Film Festival

[Cannes Film Festival](https://www.festival-cannes.com/en/) is the world's biggest film festival and market. Video NFTs and decentralisation has yet to embraced by the film industry as digital artwork has. Jules Lai met with many professionals to explain the advantages of Web3 and decentralisation with particular emphasis on ownership of content and the prospect of fairness and transparency that will emanate from that. Explaining the tools that Fabstir offers in that regard. We are in the process of partnering with a PR company to further spread the message out.

### XChaCha20 encryption added to s5client-js

XChaCha20 is a fast and secure stream cipher that is resistant to side-channel attacks. It is a good choice for applications where performance and security are critical. XChaCha20 encryption of files is working in [s5client-js](https://github.com/parajbs-dev/s5client-js); a JavaScript/TypeScript client-side API to use the content-addressed storage network S5. Fabstir uses S5 for storage on decentralised SIA cloud storage.

To encrypt, simply add `encrypt: true` in the custom options argument to s5client-js uploadFile methods and the file will be automatically encrypted before upload. S5 has service worker code so when using the downloadFile method, data will be automatically decrypted.

## Link to Repos

You'll find these listed in the Fabstir Web3 Media Player repo here: https://github.com/Fabstir/fabstir-web3-media-player/blob/main/README.md
https://github.com/julesl23/s5client-js

## What I am Working on Next

Further expand the capability of XChaCha encryption to server-side to cope with large video files that won't fit into memory.

Add this encryption feature for use in the production-ready video player that has Next.js server-side rendering.

Draw out a plan to keep Fabstir transcoder network up with cluster of NVIDIA GTX A6000 GPUs for Web3 users to use

Carry on with playback of media NFTs on Polygon/Polygon zkEVM testnets with s5 for media streaming from SIA storage, the MetaMask local storage integration to the production-ready player.

Write code that will enable compatibility for media playback for NFTs from exchanges such as OpenSea and Rarible.
