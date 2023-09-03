# Adding long play video to NFTs

By Jules Lai, Sept 2023

Hi! I'm your first Markdown file in **StackEdit**. If you want to learn about StackEdit, you can read me. If you want to play with Markdown, you can edit me. Once you have finished with me, you can create new files by opening the **file explorer** on the left corner of the navigation bar.

# Problem

According to: <a href="https://ebutemetaverse.com/can-nfts-be-videos/" target="_blank">eButem Metaverse - Can NFTs Be Videos?</a>

Video NFTs are restricted to these sizes.

OpenSea: Maximum size of 100MB
Rarible: Maximum size of 100MB
Foundation: Maximum size of 500MB
SuperRare: Maximum size of 20MB

A 100MB video file size gives approximately 1.5 mins at 1080p and around 20 secs in 4K. Not quite enough for a full-length movie. Not even enough for you average length short film.

NFT marketplaces do not transcode video formats either. Users need to upload their videos in a specified format that will work directly.

# Solution

Fabstir's media player solution allows existing NFTs to be containerised with long form video so that NFT owners are not limited by the video length anymore.

Users can take their existing video NFT from e.g. OpenSea, upload a movie-length video (or longer) in 4K resolution to it. This gets packaged together as an NFT 2.0 with ownership transferred to this. User's can set the longer video to be played by default whenever the NFT is selected to play or set to private and only viewable by the owner. A useful use case is that when on a marketplace the shorter video plays and acts like a trailer or promo but when bought, the new owner is then able to watch the longer video too.

Longer videos become much more taxing on devices for playback. Fabstir Media Player's transcoder network will receive the uploaded video and transcode it to multiple common formats that are easy to playback on the range of different hardware. Fabstir also supports transcoding to the modern higher quality AV1 codec.

All these multiple video format CIDs or urls are kept secret in MetaMask snaps encrypted storage only accessible by the owners wallet account who doesn't have to worry about these technicalities. It all happens seamlessly behind the scenes.

## NFT 2.0

Part of the new <a href="https://www.youtube.com/watch?v=nhPLzEbBaNc" target="_blank">NFT2.0 standard </a>, is ERC-6059; a standardized way to group NFTs based on the owner's preference. So an the owner could opt to have an OpenSea NFT to be in the same collection as a Fabstir video NFT. The former might represent a piece of art and the latter the making of video of that piece of art. As mentioned previously, current popular marketplaces don't support videos of more than a minute or two. Fabstir has no such video limitations. Note that this group (parent) NFT does not have to be owner of its child NFTs, only that both the child and parent owners have to agree to be in this parent collection. So use cases are very flexible.

It is a relatively new standard (an extension of the <a href="https://ebutemetaverse.com/can-nfts-be-videos/" target="_blank">ERC-721 standard</a>), created on November 15, 2022 and the proposal has only recently been accepted by the Ethereum Foundation. Hence the standard is not yet supported by the major NFT marketplaces.

<h2>References</h2>
<p><a href="https://ebutemetaverse.com/can-nfts-be-videos/" target="_blank">eButem Metaverse - Can NFTs Be Videos?</a></p>

<p><a href="https://www.youtube.com/watch?v=nhPLzEbBaNc" target="_blank">NFTs 2.0 in action: utilities, examples, and paradigm shifts</a></p>

<p><a href="https://eips.ethereum.org/EIPS/eip-721" target="_blank">ERC-721: Non-Fungible Token Standard</a></p>
