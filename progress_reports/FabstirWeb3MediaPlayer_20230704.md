# Fabstir Web3 Media Player - Progress Report (June 2023)

By Jules Lai

Added support for XChaCha20 encryption of large files to `s5client-js`. Allows for large files that might not fit in memory to be automatically encrypted client-side before upload to S5.

## Past Month Progress

### XChaCha20 encryption for large file size added to s5client-js

It took several iterations to enable large files to be encrypted client-side and reliably uploaded to S5 from the browser. Now the only limit in file size is the amount of hard drive space available, as it is possible to upload files that are too go far beyond the available memory. For example, a movie encoded in Apple ProRes 4444 can be anywhere from 150GB - 300GB+ in size. Usually would expect some sort of desktop app to be able to upload this, but it is now possible straight from the browser without installing anything.

This is done by using an internal buffer that captures the file stream from the browser, encrypts each chunk and streams the result to the Tus uploader. The internal buffer has a maximum size, and JavaScript's garbage collector deletes chunks that have already been uploaded. Tus is a resumable protocol, that makes the upload resilient to connection issues as uploads can be resumed from where it was left off etc.

XChaCha20 is a fast and secure stream cipher that is resistant to side-channel attacks. It is a good choice for applications where performance and security are critical. XChaCha20 encryption of files is working in [s5client-js](https://github.com/parajbs-dev/s5client-js); a JavaScript/TypeScript client-side API to use the content-addressed storage network S5. Fabstir uses S5 for storage on decentralised SIA cloud storage.

To encrypt, simply add `encrypt: true` in the custom options argument to s5client-js uploadFile methods and the file will be automatically encrypted before upload. S5 has service worker code so when using the downloadFile method, data will be automatically decrypted.

Added this encryption feature for use in the production-ready video player that has Next.js server-side rendering. Currently WIP.

## Link to Repos

You'll find these listed in the Fabstir Web3 Media Player repo here: https://github.com/Fabstir/fabstir-web3-media-player/blob/main/README.md
https://github.com/Fabstir/s5client-js-1

## What I am Working on Next

Carry on with playback of media NFTs on Polygon/Polygon zkEVM testnets with s5 for media streaming from SIA storage, the MetaMask local storage integration to the production-ready player.

Write code that will enable compatibility for media playback for NFTs from exchanges such as OpenSea and Rarible.
