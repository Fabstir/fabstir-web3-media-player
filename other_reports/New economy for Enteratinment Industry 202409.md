# A New Economic Model for the Entertainment Industry

**_By Jules Lai (Founder of Fabstir), Sept 2024_**

Fabstir Media Player is an open-source application that uses blockchain and Sia's decentralised storage to serve media content using Redsolver's S5 content delivery network. It allows users to create art, video and music NFTs that contain trailers, full-length video with subtitles, music with lyrics and art/posters amongst other things. These can be packaged into unique assets or collectibles within the player and sold on to other users and marketplaces.

The Fabstir Media Player helps to bring about a new economic model; one that is fairer to the content creator. The rest of this article explains how.

## The Current State of Royalties: A Disappointing Reality

The Fabstir Media Player aims to introduce a new economic model that is fairer for content creators. Currently, when a song receives 100,000 plays on a major platform, the creator only receives around $300 in royalties. In contrast, when CDs were the dominant form of music distribution, 100,000 copies would have generated around $150,000 to $225,000 for the creators. Unfortunately, with streaming platforms, the amount paid to creators and when it is paid is often at the discretion of the platform owners. They receive a large pool of money from their subscribers upfront, and are naturally incentivised to pay as little as possible back.

But how do content creators know how much they should be paid when everything is pooled together? The analytics data is hidden behind the walled gardens of the platforms, leaving creators in the dark.

## How Fabstir's New Model brings Fair Play to the Industry

Fabstir's solution works by establishing an agreement between the seller (the content creator) and the reseller (the streaming platform). If the creator agrees to the platform's standard take, for example 20%, then their NFT is automatically listed on the reseller's marketplace (permissionless). However, if the creator decides to set a fee less than 20%, then their NFT will be placed in the marketplace's pending queue, where it is up to the platform to decide whether to accept or reject it (permissioned).

With the blockchain facilitating near-instant payment at the point of sale, and its public nature and providing access to data from Fabstir's decentralised database, all parties concerned have access to the same analytics data about the content.

## Fabstir's Content State Machine

Fabstir has implemented a new way. Fabstir Media Player allows for deep integration with marketplaces that support this new model. (note that there will be another article that explains how to build such a marketplace). This model is best described to the more technical, as a state machine system...

When the Fabstir Media Player receives media from a user, this content is minted as an NFT. The NFT when submitted to a marketplace can be in any of these states:

        Accepted,
        Pending,
        Rejected,
        Deleted,
        Cancelled,
        Removed,
        Sold

- Accepted: The NFT has been accepted permissionlessly or by the platform owner.
- Pending: The seller's fees are not in line with the platform's, and they want to negotiate a better deal. It is up to the platform owners to decide whether to accept or reject the NFT for listing on their marketplace.
- Rejected: The platform owner has declined to list the seller's NFT and removed it from the pending queue. The seller can resubmit.
- Deleted: The seller has removed their NFT from the pending queue.
- Cancelled: The seller has removed their NFT from the marketplace.
- Removed: The platform owner has removed the NFT from the marketplace.
- Sold: The NFT has been sold.

Note that an ERC-721 NFT (non-fungible asset) can be in one and only one of these states as there is only one of them per asset. Whilst an ERC-1155 collectible (semi-fungible asset) can be in any or all of these states, provided the total amount in each state adds up to the total number of ERC-1155 tokens submitted to the marketplace. For example with amounts in parenthesis; Accepted(2), Pending(3), Rejected(0), Deleted(1), Cancelled(0), Removed(0), Sold(4) means that there were 10 tokens submitted in total.

## Game Theory and Fabstir's New Economic Model

Fabstir's innovative approach to the entertainment industry presents a fascinating application of game theory. By introducing a blockchain-based, decentralised ecosystem of platforms that enables everyone to sell content as NFTs, Fabstir has created a new economic model that benefits both sellers and resellers. Fabstir truly democratises streaming by allowing anyone to have their own platform, without the need for costly development or startup costs, or work withing the seller and reseller model as described here. In this section, we'll explore how game theory can help us understand the dynamics of this new model and its potential impact on the industry as a whole.

**Prisoner's Dilemma: Creators vs. Resellers**

At first glance, Fabstir's model appears to be a classic example of the Prisoner's Dilemma, where two individuals (in this case, creators and resellers) must navigate a situation where cooperation would lead to better outcomes for both parties, but individual rationality leads to suboptimal results. However, in the context of Fabstir's model, the Prisoner's Dilemma is actually resolved through the introduction of a new mechanism: permissionless listing.

**Permissionless Listing and the Tragedy of the Commons**

With permissionless listing, creators can list their NFTs on marketplaces without needing to negotiate with resellers. This eliminates the need for individual negotiations and reduces transaction costs. In game theory terms, this is an example of a "public goods" problem, where the creation and sharing of content is a collective good that benefits everyone. However, in traditional models, this leads to the Tragedy of the Commons, where intermediaries such as record labels, music publishers, and licensing companies free-ride on the efforts of creators.

**Benefits to Creators**

Fabstir's model benefits creators in several ways:

1. **Increased transparency**: With blockchain-based tracking, creators have access to accurate analytics data about their content's performance.
2. **Fairer revenue distribution**: By cutting out intermediaries and allowing creators to set their own fees and negotiate directly with resellers, Fabstir's model ensures that creators receive a fair share of the revenue generated by their content.
3. **Increased control**: Creators can choose which marketplaces to list their NFTs on and negotiate better deals with resellers.

**Benefits to Resellers**

Fabstir's model benefits resellers in several ways:

1. **Reduced transaction costs**: With permissionless listing, resellers no longer need to negotiate with creators, reducing transaction costs.
2. **Increased revenue opportunities**: By allowing creators to set their own fees and negotiate directly with resellers without intermediaries, Fabstir's model allows for discovery of new revenue opportunities for resellers.
3. **Improved content discovery**: The decentralised nature of Fabstir's ecosystem enables creators to promote their content to a wider audience whilst choosing the most appropriate platforms for their work, increasing the chances of successful sales.

**Industry-Wide Benefits**

Fabstir's innovative approach has the potential to benefit the entertainment industry as a whole:

1. **Increased competition**: By introducing the Fabstir media player and new business model, Fabstir's ecosystem of platforms increases competition in the market, driving innovation and improving services.
2. **Improved content creation**: With more creators able to monetise their work directly, Fabstir's model incentivises high-quality content creation.
3. **Decentralised governance**: The decentralised nature of Fabstir's platforms enables a more inclusive and diverse ecosystem, where creators, resellers, and marketplaces can collaborate and innovate together.

**Balancing Freedom of Expression with Responsibility: A Decentralized Solution**

Fabstir's decentralized ecosystems balance freedom of expression with responsible moderation, addressing concerns about the spread of harmful or objectionable content. By combining AI, community-driven reporting and platform moderation, Fabstir's ecosystem can identify and remove problematic content while maintaining a free and open environment. Over-censorship is not a viable solution, as it can lead to a damaged reputation and decreased user trust. Instead, Fabstir's ecosystem promotes competition among multiple platforms, allowing users freely choose where they host their content and engage with others. This approach ensures that users have choices about the level of moderation they prefer, while still maintaining a safe and respectful environment for all.

# Conclusion

Fabstir's model introduces a decentralised governance mechanism, where marketplaces set their fees and policies, while creators can also submit their own fees and policies for the marketplace to accept or not. This creates a competitive environment where marketplaces must balance their desire for revenue with the need to attract creators and maintain a healthy ecosystem. In game theory terms, this is an example of a "mechanism design" problem, where the goal is to create a set of rules that incentivise optimal behaviour from all parties involved, driving innovation and competition in the industry as a whole.
