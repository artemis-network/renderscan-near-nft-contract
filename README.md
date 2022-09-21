# Renderscan-near-nft-contract

This is a basic NFT smart contract on NEAR blockchain. NEAR NFT smart contract standards have been maintained. We followed NEP-171 and NEP-177 standards. The NEP-171 & NEP-177 standards explain the minimum interface required to be implemented, as well as the expected functionality.

Our NFT smart contract allows users to mint an NFT on NEAR blockchain. Since it is integrated with our Renderscan app, users can create wide range of NFTs by simply clicking mint button in the app, which triggers the "nft_mint" method in this contract. Users can also chose to create collections by creating N number of NFTs with the same metadata but different tokenID.

**The following features are supported by the NEAR NFT smart contract**

 1. **Minting NFTs and Collections** - Can Mint single NFT or a collection of NFTs
 2. **Checking Metadata** - There is a viewmethod called "check_token" to verify the metadata of an NFT
 3. **Royalties** - You can be eligible to receive royalties that will be paid automatically when a NFT token is sold in marketplace
 4. **Authorizing users** - You can grant other users permission to transfer an NFT that you own. This is useful for       listing your NFT in a marketplace, for example. In such scenario, you trust that the marketplace will only transfer the NFT upon receiving a certain amount of money in exchange.
5. **Transfer NFT** - NFT can be transferred in two ways. 1) you can request an NFT transfer 2) An authorised account requests the transfer of an NFT. In both instances "nft_transfer" method should be invoked

# Quick-Start

```
git clone https://github.com/artemis-network/renderscan-near-nft-contract
cd renderscan-near-nft-contract
yarn build
```
## Deploy Contract

    near deploy --accountId $NFT_CONTRACT_ID --wasmFile out/main.wasm

## Initialize Contract

    near call $NFT_CONTRACT_ID new_default_meta '{"owner_id": "'$NFT_CONTRACT_ID'"}' --accountId $NFT_CONTRACT_ID

## Checking metadata

    near view $NFT_CONTRACT_ID nft_metadata

## Minting Token

    near call $NFT_CONTRACT_ID nft_mint '{"token_id": "token-1", "metadata": {"title": "My Non Fungible Team Token", "description": "The Team Most Certainly Goes :)", "media": "https://bafybeiftczwrtyr3k7a2k4vutd3amkwsmaqyhrdzlhvpt33dyjivufqusq.ipfs.dweb.link/goteam-gif.gif"}, "receiver_id": "'$MAIN_ACCOUNT'"}' --accountId $MAIN_ACCOUNT --amount 0.1

## View NFT Info

    near view $NFT_CONTRACT_ID nft_token '{"token_id": "token-1"}'

## Transfer NFTs

    near call $NFT_CONTRACT_ID nft_transfer '{"receiver_id": "$MAIN_ACCOUNT_2", "token_id": "token-1", "memo": "Renderverse)"}' --accountId $MAIN_ACCOUNT --depositYocto 1
