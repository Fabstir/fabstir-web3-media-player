# Fabstir Web3 Media Player - Progress Report (Jul 2023)
By Jules Lai

Rust transcode server can receive encrypted video files from S5 for transcoding. The transcoder can transcode from a source video to multiple file formats given a list of video format specifications. WIP media player has functionality to display a gallery of video/audio NFTs and use MetaMask to unlock those owned for playback.

## Past Month Progress

[1]: Added the ability to download encrypted files from S5 in Rust. This is now used in the transcoder server for downloading encrypted original source media.

[2]: Another addition is that the transcoder now reads a JSON file that has a list of settings that describes the parameters for `ffmpeg` to determine the transcoded video/audio formats to export. This can range from different output codecs (usually AV1 and h264 for video), at different resolutions (1080p, 4K etc.), at different bitrates (slow to high), with different audio bit rates etc. Here are two example entries:
```
[
    {"id": 31, "label": "1080p", "type": "video/mp4", "ext": "mp4", "vcodec": "libx264", "preset": "medium", "profile": "main", "ch": 2, "vf": "scale=1920x1080", "b:v": "1.25M", "ar": "44k", "gpu": true},
    {"id": 34, "label": "2160p", "type": "video/mp4", "ext": "mp4", "vcodec": "av1_nvenc", "preset": "slower", "profile": "high", "ch": 2, "vf": "scale=3840x2160", "b:v": "18M", "ar": "48k", "gpu": true}
]
```
Note that each transcoded video format is described by a `label` property that can be displayed in a media player menu bar to allow the user to choose different resolutions or some other criteria.

[3]: Added helper functions to [s5-encryptWasm](https://github.com/Fabstir/s5-encryptWasm) repo including `getKeyFromEncryptedCid` that can remove the key portion from an S5 CID that points to an encrypted file.

[4]:  Work-in-progress (not complete) dapp Web3 media player to play video and music NFTs [ERC-721](https://ethereum.org/en/developers/docs/standards/tokens/erc-721/) whose media content is stored in S5. Uses [MetaMask Snaps](https://metamask.io/snaps/) to hold the key portion of the CID  in MetaMask wallet's sandboxed local storage whilst the rest of the CID (the portion without the key) is in the NFT's metadata publicly stored in S5, where the CID to this unencrypted metadata is stored on the blockchain. In order to get access to play the NFT's media, a user would need to unlock their MetaMask wallet first. Once that is done, the media player dapp can then use the wallet's Web3 API to access the key of the NFT's content. Combining this with the NFT's metadata that has the CID without the key, gives the full CID to the content stored on S5 that the dapp can now play.
The gallery displays NFTs as tiles where their images are loaded lazily using Next.js <image> tag.


## Link to Repos

You'll find these listed in the Fabstir Web3 Media Player repo here: https://github.com/Fabstir/fabstir-web3-media-player/blob/main/README.md
 https://github.com/Fabstir/s5-encryptWasm
 https://github.com/Fabstir/media-player.git

## What I am Working on Next

Complete the dapp media player.

Enable NFTs from exchanges such as OpenSea and Rarible to be ingested in, so that their content  can be transcoded and stored to S5 for secure smooth playback on multiple devices.
