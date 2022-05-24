<img src="https://user-images.githubusercontent.com/33762147/155625647-55c69f06-e0ea-44a8-a425-7aa086c329c5.png" style="border-radius:50%;width:72px;">

# Smart Contracts for SigmaFi APY NFT Minter

## Summary

This application locks up SDEX or SDEX LP tokens for a user selected period of time, after the timeframe has exceeded the selected period, the user will be allowed to mint an APY NFT with no penalty to their stake. APY NFT values increase daily depending on the amound of SDEX or LP tokens staked.

APY NFTs can be used in conjunction with staking SDEX in other SigmaFi pools to earn rewards relative to their minted NFTs.

**Eg.** John bought and staked 50,000 SDEX in the NFT Minter Contract for 365 days. The contract credits him 0.000015 per SDEX per day giving him an increase of 0.75% per day for 1 year (365 days). After his contract reaches maturity, he can mint an APY NFT for 273% and obtain all his staked SDEX he put up in order to mint his NFT. After John mints his NFT he has two options to capitalize on the opportunity:
* He can sell the NFT for an instant profit
* He can stake SDEX to recieve 273% APY in rewards relative to his capital

## Proposed Variables
<div align="center">
  
|multiplier|value|
|-------------|--------|
|SDEX daily   |0.000015|
|SDEX LP daily|0.000050|
  
</div>
  
# Proposed Flow Diagram

<p align="center">
<img src="https://user-images.githubusercontent.com/33762147/170084813-5bd49f1b-aba4-427b-b4fd-3b410ac35883.png" style="width:560px;">
</p>
