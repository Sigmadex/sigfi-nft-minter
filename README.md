<img src="https://user-images.githubusercontent.com/33762147/155625647-55c69f06-e0ea-44a8-a425-7aa086c329c5.png" style="border-radius:50%;width:72px;">

# Smart Contracts for SigmaFi APY NFT Minter

## Summary

This application locks up SDEX or SDEX LP tokens for a user selected period of time, after the timeframe has exceeded the selected period, the user will be allowed to mint an APY NFT with no penalty to their stake. APY NFT values increase daily depending on the amount of SDEX or LP tokens staked.

APY NFTs can be used in conjunction with staking SDEX in other SigmaFi pools to earn rewards relative to their minted NFTs.

**Eg.** John bought 50,000 SDEX from a DEX and staked the entire 50,000 SDEX in the NFT Minter DAPP for 365 days. The DAPP contract credits him 0.000015 per SDEX per day giving him an increase of 0.75% per day for 1 year (365 days). After his contract reaches maturity, he can mint an APY NFT for 273% and obtain all his staked SDEX he put up in order to mint his NFT. After John mints his NFT he has two options to capitalize on the opportunity:
* He can sell the NFT privately or on a secondary marketplace for an instant profit
* He can stake SDEX in another DAPP to recieve 273% APY in rewards relative to his capital

If the contract has not reached maturity and `withdraw` is called, a penalty to the principal will be applied based on boostrap variables shown below.

## Proposed Genesis Parameters
Variables for both rewards and penalties will be set by the contract deployer only and can be modified by the deployer at anytime.

### Initial Reward Variables
When commitments are respected, rewards are given for loyalty.
<div align="center">
  
|desc|value|var|
|-------------|--------|-----------|
|SDEX daily   |0.000015|`sdexAPY`  |
|SDEX LP daily|0.000050|`sdexlpAPY`|
  
</div>

### Initial Penalty Variables
Penalties are an ecosystem balancing mechanism.
<div align="center">
  
|penalty|value|var|desc|
|-------------|--------|----------|-----------|
|SDEX daily   |50%|`sdexPenalty`  |SDEX burn pool|
|SDEX LP daily|50%|`sdexlpPenalty`|LP tokens forfeited into treasury|
  
</div>

### Variables

<div align="center">
  
|query|type|desc|
|-------------|--------|-------|
|`auth`         |*address*|Address of the contract deployer|
|`sdexPenalty`  |*unit256*|Penalty rate to be set by `auth`|
|`sdexlpPenalty`|*unit256*|LP tokens forfeited into treasury to be set by `auth`|
  
</div>
  
## Example Scenario

1. User uses react front-end to timelock and deposit SDEX or SDEX LP tokens into minter 
2. Deposit data is stored on-chain in an [array](https://github.com/Sigmadex/sigfi-nft-minter/blob/main/README.md#proposed-array-format)
3. `isLiquidity` is set to 0 if SDEX is deposited or 1 if SDEX LP is deposited
4. As time elapses the daily NFT rate is derived from multiplying the amount of SDEX staked by `sdexAPY` once per day
5. `mint` is called by the user and the current `timestamp` is > than `endTimestamp` 
6. The minter contract returns the staked SDEX to the users wallet and mints the APY NFT to their wallet
  
### Proposed Array Format

<div align="center">

|wallet|staked|minedAPY|startTimestamp|endTimestamp|isLiquidity|
|-------------|--------|--------------|------|-----|-----------|
|0x82C879fdBd65aD36f8Fccc...|50000|0.17|55469846561|83469846588|0|
  
</div>

### Storage Variables

<div align="center">
    
|query|type|desc|
|-----|----|----|
|wallet|*address*|Address of wallet which staked tokens|
|staked|*uint256*|Number of tokens which are held in the smart contract for this specific `wallet`|
|minedAPY|*uint256*|Current NFT value, updated once per day|
|startTimestamp|*uint256*|Time of when the position was opened|
|endTimestamp|*uint256*|Time of when the position will mature and `mint` can be called without penalty|
|isLiquidity|*bool*|Identifies whether the deposit is an LP token or SDEX, 1 = *yes* 0 = *no*|

</div>
    
## Proposed Flow Diagram
<p align="center">
<img src="https://user-images.githubusercontent.com/33762147/170894657-45ae3957-4503-4b67-aa19-6d9acbaa742c.png" style="width:560px;">
</p>

## Figma

![2022-06-09_22-57-55](https://user-images.githubusercontent.com/33762147/172994575-686558e2-b95d-461c-9bf1-6e2ccb91a529.jpg)
