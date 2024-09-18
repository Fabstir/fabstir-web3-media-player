# Fabstir Media Player

By Jules Lai, Sept 2024

## Supported Features for Minimum Viable Product (MVP) Release

### Trailers

Trailer files are saved to lower quality footage on IPFS for compatibility, enabling them to be viewed in most non-fungible token (NFT) marketplaces. Once purchased, the new owner can watch the full movie or listen to the entire song within Fabstir Media Player, which streams the transcoded media from Sia storage in higher quality 1080p or 4K via Resolver's S5. Resolution is selectable from the player toolbar.

### Subtitles

Fabstir Media Player supports .vtt file format subtitles. The languages can be easily selected from the player's toolbar when playing the NFT video.

### Lyrics

Lyrics in .lrc format can be added to audio and minted as an audio NFT. Lyrics playback in sync with the music.

### Foreign Languages

NFT videos minted by the player support multiple audio tracks, enabling different languages; the original audio and dub tracks. All these audio tracks and their various bit rates are streamed from Sia storage via Resolver's S5.

### TV Shows and Boxsets

Similar to the days of Blu-ray and DVD boxsets of TV series, NFTs can be grouped together into a collectible and sold as a unit on a marketplace that supports RMRK NFT 2.0 standard. The structure is held together via smart contracts on the blockchain. Fabstir Media Player displays boxsets as hierarchical thumbnails in its gallery. Clicking on any thumbnail reveals the episodes inside the boxset or series, represented as individual thumbnails that can be clicked and watched.

### Individual Assets vs Semi-Fungible

Fabstir Media Player supports unique assets represented as ERC-721 NFTs for assets where there is only one unique version, such as NFT art. The player also supports semi-fungible assets via the ERC-1155 standard. For example, when selling songs, you are able to mint a fixed supply of the same song that can be bought individually by fans.
In the player's gallery area, which lists the digital assets that the user owns and can play back at any time, the assets can be non-fungible or semi-fungible.

### Sia vs IPFS

NFT metadata, images, and data files can all be saved to Sia storage supporting S5's cid addressing. By default, these are saved to IPFS for maximum compatibility with marketplaces. However, higher storage or bandwidth data and media are saved and streamed from Sia storage only.
General indexable data is stored on IPFS via FabstirDb graph database; once Redsolver has finished S5 specs for Rust, plan is to use Sia for underlying storage for the graph database.

### Marketplaces vs Custom Marketplaces

Any NFTs that Fabstir Media Player mints can be sold on common marketplaces like OpenSea, Rarible, etc. Where samples and trailers can be viewed. The new owner is then able to play the full content in Fabstir Media Player.
The player supports tight integration with Fabstir's custom marketplaces. Here, the seller is able to set limitations on how much fee the reseller marketplace is able to take from sales. Custom marketplaces are also able to set the fee percentage that they require in order to gain access for permissionless listings. Either party can accept or reject terms, making the process more democratic.
To implement your own custom marketplaces, the interfaces and events required by the player to operate are available on a Fabstir GitHub repository. Custom marketplaces support buy now and auction transactions.

### Transcoding

Fabstir Media Player supports multiple playback devices with different resolutions and bit rates. The player transcodes uploaded media to multiple formats and saves them to Sia storage. On playback, the user can choose which format to stream, best suited to their needs from the player's toolbar or leave it to default.
