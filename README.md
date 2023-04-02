
# Fabstir Web3 Media Player

If you are a film and music lover like I am then hopefully you will appreciate this player. It allows you to own content again, like in the days of physical media (remember CDs, Vinyl or Blu-rays)?

Currently the subscription model is dominant, so one can watch or listen to content so long as you are subscribed to a platform's subscription service. Meaning, the moment your subscription is cancelled then all the content you had access to is gone and you can no longer consume any of it. Also, the platform can add and remove content however it chooses. So particular content you thought you had access to can be removed at anytime.

With a digital wallets, thanks to blockchain technology, once again you can own content to consume whenever desired. Providing your private key is kept safe, then your media collection cannot be taken away from you.

This player will both stream from decentralised storage and store permanently to decentralised storage. 


# Work to do done

This list serves as a reminder and sanity check that there is a lot of work to be done.

## GPU transcoding
Surprisingly there is not a lot of decentralised compute networks available that offers video encoding. This project will be leveraging both centralised and decentralised networks. The former for low cost modern GPU acceleration especially for AV1 (royaly free) and JPEG2000 codecs. The latter for censorship resistance, fallback etc.

## Digital assets
Away from the hype, NFTs serve a real solution to the problem of uniquely identifying digital assets. Hence it's name non-fungible token. If you have an NFT in your digital wallet account, this would usually mean that you own it and the contents that it is pointing to.
Fabstir Web3 Media Player makes this easier for the consumer by directly integrating into Web3 wallets such as MetaMask, to provide a more seamless experience.

## Decentralised storage
Media is too expensive to store on most blockchains so it is stored off-chain on decentralised storage that an NFT then points to. The media content is hashed to uniquely identify it, so if anyone were to tamper with it then its hash will no longer match up. For data integrity, security and censorship resistance, decentralised storage services such as SIA and Arweave have the answer.

## Content delivery network
Content delivery networks (CDNs) help to improve the performance and availability of media by replicating it on servers that are closer to the end users and by offloading traffic from the origin server. This project intends to use S5 from Redsolver and Lume from Derrick Hammer, to provide CDN streaming from SIA storage. The media player will also enable content caching of other storage solutions such as from IPFS and Arweave onto SIA for smooth streaming across different devices and networks.

## Archiving
Blu-rays and CDs/Vinyl's had a physical shelf-life. Permanence of media can now be improved upon still further; Arweave's incentive model with their decentralised networks can help guarantee storage forever. It is intended that Fabstir Web3 Player to allow user's content to be stored there; including movies in DCP (Digital Cinema Package) format that reflect the culture in which they are made, and can provide a snapshot into the values, beliefs, and customs of a particular society at particular time.

# The Project State
A lot of the tech has already been built and exists in Fabstir (platform). The technology whitepaper is here: https://www.fabstir.com/files/Fabstir_whitepaper_20221012.pdf
We are looking at smart contracts in Solidity running on Polygon. The technology stack is Typescript, React, NextJS with WASM for tasks like audio encoding, C++ for GPU encoding/transcoding of video.

Many thanks to SIA Foundation for a grant (https://blog.sia.tech/grants-program-update-december-2022-f7be5f103d13) to help fund this mission.

# Licensing 
This project is FOSS (free and open source software) under MIT license.

# Web3 goals
Fabstir's goal is to use Web3 technology to allow for a fairer society:

 - Having a Web3 media player on popular digital wallets allows media lovers to buy NFT media content directly from creators to keep and to enjoy streaming straight out of their wallet account. This allows content creators to receive the majority of the income and keep their content rights too, as there can be far fewer intermediaries. Content creators would be now top of the food chain and be able to fund their next projects more easily!
 - With Web3, everything can be more open and transparent as transaction history is available on the blockchain. Thus, breaking down the walled gardens prevalent in the media industry. Content creators are able to negotiate better deals as budgets and income will become more transparent allowing standards to form.
 - Less intermediaries, means less distance between content creators and what fans want.  Community driven content can thrive allowing for much more diverse and exciting content from around the world. Creators can produce content true to their vision rather than have to fit into branding.
 - Cinemas have taken a hit since subscription platforms are focusing on their own productions that often bypass theatrical release entirely, as their goal is to attract more subscribers. Fabstir Web3 media player will make it easy for independent filmmakers to access directly digital cinemas and film festivals, using digital wallets to securely deliver the film to cinema projectors. Potentially skipping layers of intermediaries and opening a new market for cinemas to gain content that can be difficult to get hold of through traditional distribution channels.

These are just some of the benefits Web3 can bring to the media industry that Fabstir aims to deliver.

# Relevant Repos

A [test video player  app](https://github.com/Fabstir/upload-play "The video player is a JavaScript test app. Allows users to upload videos to decentralised storage.") and [deployment files](https://github.com/Fabstir/upload-play-infra "Uses continuous integration and deployment") 
A [test video transcoder server](https://github.com/Fabstir/transcode "Transcodes uploaded videos to 1080p and 720p h264 m4 formats to decentralised storage for playback by test video player.") and [deployment files](https://github.com/Fabstir/transcode-infra "Uses continuous integration and deployment")
A test [MetaMask Snaps application](https://github.com/julesl23/playlist-example, "Allows a wallet owner to add blockchain addresses into MetaMask Snaps's encrypted local storage")

The repos use continuous integration and deployment to the cloud using GitHub Actions and Docker.
