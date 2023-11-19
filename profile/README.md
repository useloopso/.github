# Loopso

First **cross-chain**, **bi-directional** bridge on [Lukso](https://lukso.network/), agnostic to token types, and txs confirmed within 30 seconds ✌️ 

<div align="center">
<img 
  src="https://github.com/useloopso/.github/raw/prod/assets/square-logo.png" 
  style="width:40% ; height:40%;"
/>
</div>

## 📖 Table of Contents
1. [Smart contracts](#smart-contracts)
2. [Relayer](#relayer)
3. [SDK](#sdk)
4. [Frontend](#frontend)
5. [Roadmap](#roadmap)
6. [Limitations](#limitations)

### Smart contracts
Transfer tokens between Sepolia, Lukso Testnet, and Mumbai by locking them on the source chain, triggering a rapid minting process on the destination chain through a centralized Bridge Messaging Relayer.

#### Core Mechanism
- Users lock tokens on chain A, and a relayer mints corresponding tokens on chain B.
- Applicable to any tokens in both directions.
-  Architecture inspired by Wormhole, prioritizing security.


#### Deployed Chains
- Deployed on Sepolia, Lukso Testnet, and Mumbai.
- Community-selected networks based on this [poll](https://x.com/loopso_xyz/status/1725529010535371236).

#### Example Bridging Process
1. A user initiates the bridging process by calling `bridgeTokens(uint256 _amount, address _to, bytes32 _tokenID)`, specifying the amount, destination address, and the recorded attestation's _tokenID.
2. The bridge deducts the specified token amount from the user's balance.
3. An event `TokensBridged` is emitted, including the transfer ID.
4. The relayer uses the transfer ID to obtain transfer details from the bridge and performs necessary verifications.
5. The relayer calls `releaseWrappedTokens` on Chain B.
6. Chain B mints the specified amount of wrapped tokens and emits an event, notifying the user of the successful bridging process.
7. If the user intends to bridge back, they call `bridgeTokensBack`, burning the specified amount of wrapped tokens.
8. An event `TokensBridgedBack`, similar to `TokensBridged`, is emitted.
9. The relayer picks up the event, calls `releaseTokens` on Chain A, and transfers the specified token amount back to the user.