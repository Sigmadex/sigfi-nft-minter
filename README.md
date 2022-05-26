<img src="https://user-images.githubusercontent.com/33762147/155625647-55c69f06-e0ea-44a8-a425-7aa086c329c5.png" style="border-radius:50%;width:72px;">

# Smart Contracts for SigmaFi APY NFT Minter

## Summary

This application locks up SDEX or SDEX LP tokens for a user selected period of time, after the timeframe has exceeded the selected period, the user will be allowed to mint an APY NFT with no penalty to their stake. APY NFT values increase daily depending on the amound of SDEX or LP tokens staked.

APY NFTs can be used in conjunction with staking SDEX in other SigmaFi pools to earn rewards relative to their minted NFTs.

**Eg.** John bought 50,000 SDEX from a DEX and staked the entire 50,000 SDEX in the NFT Minter DAPP for 365 days. The DAPP contract credits him 0.000015 per SDEX per day giving him an increase of 0.75% per day for 1 year (365 days). After his contract reaches maturity, he can mint an APY NFT for 273% and obtain all his staked SDEX he put up in order to mint his NFT. After John mints his NFT he has two options to capitalize on the opportunity:
* He can sell the NFT for an instant profit
* He can stake SDEX to recieve 273% APY in rewards relative to his capital

## Proposed Genesis Parameters
Variables for both rewards and penalties will be set by the contract deployer only and can be modified by the deployer at anytime.

### Reward Variables
When commitments are respected, rewards are given for loyalty.
<div align="center">
  
|desc|value|var|
|-------------|--------|-----------|
|SDEX daily   |0.000015|`sdexAPY`  |
|SDEX LP daily|0.000050|`sdexlpAPY`|
  
</div>

### Penalty Variables
Penalties are an ecosystem balancing mechanism.
<div align="center">
  
|penalty|value|var|desc|
|-------------|--------|----------|-----------|
|SDEX daily   |50%|`sdexPenalty`  |SDEX burn pool|
|SDEX LP daily|50%|`sdexlpPenalty`|LP tokens forfeited|
  
</div>
  
## Example Scenario

1. User uses react front-end to timelock and deposit SDEX into minter contract data is stored in an array
2. As time elapses the daily NFT rate is derived from multiplying the amount of SDEX staked by `sdexAPY` once  day
3. A sufficent time elapses and `mint` is called by the user
4. The minter contract returns the staked SDEX to the user and mints the APY NFT to their wallet
  
### Proposed Array Format
<div align="center">

|wallet|staked|totalAPY|endTimestamp|
|-------------|--------|-----------|
|0x82C879fdBd65aD36f8Fccce3AF6cd5b5E757fD03|50000|0.17|55469846561|

</div>
  
## Proposed Flow Diagram
<p align="center">
<img src="https://user-images.githubusercontent.com/33762147/170386375-8f26cc01-7c99-414c-b578-af8d90d4b70b.png" style="width:560px;">
</p>
