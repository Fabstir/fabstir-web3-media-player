<h2>Fabstir Web3 Media Player - Progress Report (Oct 2023)<h2>
by Jules Lai

<h4>What progress was made on your grant this month?<br>
Please summarize your progress in 3-5 sentences or bullet points:</h4>

_Added 3d rendering capability to Fabstir Media Player.
Fabstir Renderer displays 3d models from .gltf files in real-time. It currently supports direct lighting, textures, vertices and polygons. It is cross-platform compatible as it uses WGPU under the hood. No install necessary, works straight from the browser._

_Added ERC-7409 Nestable NFTs to Fabstir Media Player. Upgraded from ERC-6059 as ERC-7409 now supercedes it. Decided against ERC-5773 for now as not backwards compatible with existing NFTs_

_Worked with developers of social media login and accounts abstraction libraries for bug fixes and improved UI experience_

Links to repos worked on this month:

- _[Fabstir_Media_Player_Snaps](https://github.com/Fabstir/Fabstir_Media_Player_Snaps/tree/main/packages/site)_
- _[Fabstir_Renderer](https://github.com/Fabstir/fabstir-renderer.git)_

<h4>What will you be working on this month?<br>
Please summarize your development goals into a few sentences or bullet points:</h4>

- _UI tidying and improved documentation for Fabstir Media Player_
- _More testing, improve lighting, and relative positioning for nested NFT 3d models_
- _Improve error handling for Fabstir Transcoder_
