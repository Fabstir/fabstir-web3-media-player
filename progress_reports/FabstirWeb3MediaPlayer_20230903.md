<h2>Fabstir Web3 Media Player - Progress Report (Sept 2023)<h2>
by Jules Lai

<h4>What progress was made on your grant this month?<br>
Please summarize your progress in 3-5 sentences or bullet points:</h4>

_The Fabstir Media Player now works as a MetaMask Snaps extension using its secure vault environment to securely store details of NFT addresses, any encryption keys and video formats. The Next.js, React, Tailwind css decentralised application enables these NFTs to be displayed in a gallery, using advanced caching when loading NFT metadata from the blockchain, and will lazily load images from s5 (Sia) as they enter the viewport to speed up performance. Clicking on an NFT brings it up in a side panel where images are displayed in a larger format and any videos can be played and watched up to full-screen. Support for very long NFT videos up to 4K resolution, automatically transcoding for smooth playback from s5 (Sia) across a multitude of different devices._

Links to repos worked on this month:

- _[Fabstir_Media_Player_Snaps](https://github.com/Fabstir/Fabstir_Media_Player_Snaps/tree/main/packages/site)_
- _[The snap base layer](https://github.com/Fabstir/Fabstir_Media_Player_Snaps/tree/main/packages/snap)_
- _[Fabstir/transcode](https://github.com/Fabstir/transcode)_
- _etc._

<h4>What will you be working on this month?<br>
Please summarize your development goals into a few sentences or bullet points:</h4>

_Currently expanding Fabstir Media Player to enable long-form videos to be added to NFTs from popular marketplaces like OpenSea and Rarible that limit their videos to 100MB. This is done by repackaging them using Fabstir's limitless length videos into the new NFT 2.0 standard. Use cases include using the shorter video as a trailer or promo video, then the long video would be the actual movie. Or can have an NFT image, where the long-form video could be the "making of the art content"._
