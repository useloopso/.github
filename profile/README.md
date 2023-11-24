# Loopso

First **cross-chain**, **bi-directional** bridge on [Lukso](https://lukso.network/), agnostic to token types, and txs confirmed within 30 seconds ✌️

<div align="center">
<img 
  src="https://github.com/useloopso/.github/raw/prod/assets/square-logo.png" 
  style="width:40%; height:40%;"
/>
</div>

## 🔓 Why is a Bridge important?
Bridges connect **digital communities**, **exchanging value** between networks and fostering **growth** in areas like community, developer engagement, and overall awareness — **critical for Lukso**.

## 📚 Summary
Transfer tokens between **Sepolia, Lukso Testnet, and Mumbai** by locking them on the source chain, triggering a rapid minting process on the destination chain through a centralized **Bridge Messaging Relayer**.

### ⚙️ Core Mechanism
- Users lock tokens on chain A, and a relayer mints corresponding tokens on chain B.
- Applicable to any tokens in both directions.
-  Architecture inspired by Wormhole, prioritizing security.


### ⛓️ Deployed Chains
- Deployed on Sepolia, Lukso Testnet, and Mumbai.
- Community-selected networks based on this [poll](https://x.com/loopso_xyz/status/1725529010535371236).

### 🪜 Example Bridging Process for Fungibles
1. A user initiates the bridging process by calling `bridgeTokens(uint256 _amount, address _to, bytes32 _tokenID)`, specifying the amount, destination address, and the recorded attestation's _tokenID.
2. The bridge deducts the specified token amount from the user's balance.
3. An event `TokensBridged` is emitted, including the transfer ID.
4. The relayer uses the transfer ID to obtain transfer details from the bridge and performs necessary verifications.
5. The relayer calls `releaseWrappedTokens` on Chain B.
6. Chain B mints the specified amount of wrapped tokens and emits an event, notifying the user of the successful bridging process.
7. If the user intends to bridge back, they call `bridgeTokensBack`, burning the specified amount of wrapped tokens.
8. An event `TokensBridgedBack`, similar to `TokensBridged`, is emitted.
9. The relayer picks up the event, calls `releaseTokens` on Chain A, and transfers the specified token amount back to the user.

## ♾️ Products
- **Smart contracts**: Solidity contracts for the Loopso bridge deployed on each chain. 
- **Relayer**: A Bridge Messaging Relayer (BMR) designed to read on-chain events & execute functions.
- **SDK**: A lightweight npm package for developers to embed into their dApp for easy cross-chain bridging.
- **Frontend**: A NextJS frontend used to seamlessly bridge fungible and non-fungible tokens.
- **Foundry library**: A lightweight library that makes it easier to work with LSP7 and LSP8 smart contracts in Foundry.
- **Transaction Relayer**: Subsidize gas on behalf of Lukso users only.


## 💎 Features
- Bridge between ERC20 <> LSP7 and ERC721 <> LSP8.
- Programmatically allow any developer to use our bridge easily with our SDK: Enabling decentralized front-ends, or programmatically bridging without a UI.
- A clean UI to enable any user to seamlessly move funds between networks.
- Take fees on fungible tokens and a cost to bridge for non-fungibles.
- Developers on Lukso can use our LSP7 and LSP8 library when they use Foundry.
-  A 24/7 bridge relayer that mints and redeems.
-  Transaction relayer that subsidizes user gas (exclusive to Lukso).

## 🏗️ Roadmap & Limitations
- Currently, there is one centralized BMR that can be prone to outage and downtime. A single point of failure in the server could stop it, but we have plans for multi-relayer support. A decentralized group of relayers that work together to prevent that single point of failure.
- Frontend UX could be better, especially as we have different wallets.
- Bridge between native tokens on each chain (e.g. LYXe <> LYX).    
- Internal Bridge Block Explorer.