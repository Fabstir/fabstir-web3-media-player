
# Fabstir Web3 Media Player - Progress Report (Mar 2023)
By Jules Lai

Over the past month, a cloud-based infrastructure and test MetaMask Snaps app have been<br>
developed. The infrastructure comprises two clusters for media playback and video transcoding,<br>
communicating via gRPC and utilising load balancing. Both clusters are hosted on Akamai, with<br>
multi-cloud support. The MetaMask app allows users to manage their NFT addresses within a<br>
secure environment, storing encrypted data locally and offering backup storage on SIA. Currently<br>
working on the production-ready Web3 video player with enhanced features.

## Past Month Progress

[1]: Deployed a test infrastructure up in the cloud:

Cluster #1 two nodes running ExpressJS simple media player application.

Cluster #2 two nodes running a Rust server for performing the video transcoding services.

Cluster #1 communicates with Cluster #2 via gRPC. So very easy to use programmatically, for IntelliSense for the gRPC API, that can use e.g. the Protocol Buffer Language Support extension for Visual Studio Code, that provides syntax highlighting, code completion, and other features for protobuf files.

Cluster #2, uses a `loadbalancer` to ensure that transcoding workload is evenly distributed among the available compute notes. Transcoded footage is then stored to SIA storage via S5 content-addressable network.

Both clusters run on Akamai cloud service provider (https://www.akamai.com/ ). As the infrastructures are designed to be multi-cloud, other providers will be supported.

[2]: Test MetaMask Snaps written and working.

The MetaMask app uses TypeScript to implement a running application within a sandboxed environment with MetaMask Flask (a developer version of MetaMask digital wallet).

The test allows a wallet owner to add all their NFT addresses that they own into MetaMask. Within a secure sandboxed environment, the test application runs and calls on MetaMask to store the list of addresses using the user's private credentials to encrypt to local storage. There will be a backup feature to securely store these addresses to SIA, so that a user is able to access their NFT collection from any device, providing that they have access to the account.

Initially I had a problem implementing this, but a MetaMask dev pointed out the error in my ways and now the test app is fully working.

[3]: In terms of the proposed project timeline, both HLS format and MEG-DASH format that has yet not been tested as these formats are not as efficient on S5 as large contiguous files are that are already Blake3 encrypted anyway. This may be different of course when LumeWeb has available its content-addressable network. Tests so far have transcoded video to multiple bit rates and resolutions for successful storage and streaming of video files with the test player.

## Link to Repos

You'll find these listed in the Fabstir Web3 Media Player repo here: https://github.com/Fabstir/fabstir-web3-media-player/blob/main/README.md

## What I am Working on Next

Currently working on the production-ready video player. This is using a technology stack that includes React, JavaScript/TypeScript, Tailwind, Snaps and Solidity smart contracts. It features support for multiple playback speeds and subtitles. For audio, there is support for .lrc lyric format.
