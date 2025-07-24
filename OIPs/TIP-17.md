| id | Title | Status | Author | Description | Discussions to | Created |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| TIP-17 | THALES L2 Gamified Staking| Implemented | Danijel (@dgornjakovic) | Define gamified THALES approach on L2| https://discord.gg/8bzFdpGTrp | 2021-12-29
 
## Simple Summary
 
The TIP aims to formalize a plan on how rolling out THALES token on Optimism mainnet will be conducted. 
 
## Motivation
  
Thales has been rewarding 125k THALES rewards to SNX users pro rata based on the SNX staking debt on a weekly level. While this number is a large portion of THALES inflation, it did not make a significant impact on Synthetix staking due to the large TVL in SNX staking and it hardly makes a difference to an average SNX staker. This TIP proposes to reduce that total number of weekly rewards for SNX stakers, while reverting the value of that inflation to THALES staking. To achieve this SNX staking will have a significant weight in the new gamified THALES staking approach that provides a bonus to stakers based on certain parameters.  
Furthermore, this TIP aims to improve Thales Staking module by offering a gamified approach to staking which rewards active protocol users.    

## Specification
Thales wants to make DeFi feel like playing a game. Instead of having ad hoc incentives programs for each product rollout, Thales wants to try on ongoing approach that ties usage of the protocol to bonus rewards paid for staking THALES.


Gamified THALES staking on Optimism Mainnet:
- Base weekly rewards of 70k THALES
- Introduce a bonus with a maximum value of 30% on top of base rewards that is calculated based on the following:  
      - 50% based on SNX staking. If a THALES staker has at least 1 SNX staked per THALES he would receive as base reward, he gets maximum bonus, otherwise he gets proportional to the SNX he has staked   
      - 40% weight to AMM trading volume. If a THALES staker has at least 10 sUSD AMM volume in last 4 epochs per 1 THALES he gets as base reward, he gets maximum bonus in this category, otherwise he gets a bonus proportional to the average volume he generated in the last 4 epochs divided by the base THALES rewards he is eligible to receive.    
      - 10% weight if the staker participated in the last or ongoing Thales Royale. This value can be either 0 or max.

`Amount of SNX staked` is not a direct variable that can be fetched from Synthetix contracts given that cRatio fluctuates with SNX price movements. Instead, this TIP proposes to use a normalized SNX staked value that calculates the SNX staked based on the current amount of debt per wallet and its cRATIO.       
      
On Optimism Mainnet rewards will have to be claimed weekly and be subject to same escrow rules as in the staking contract on Ethereum Mainnet.
Further improvements to staking can be formalized in additional TIPs.
 

## Test Cases
A THALES staker is staking 5200 THALES. Current APR is exactly 100% for base rewards so he is eligible to get 100 THALES as base rewards.  
He can get an additional 30 THALES bonus if he meets the following criteria:
- 15 THALES if he has at least 100 SNX staked at normalized cRatio. If he has less SNX staked he gets `amountSNXStaked/100 x 15`
- 12 THALES if he did 1000 sUSD volume via AMM in last 4 period. If he did less he gets `amountTraded/1000 x 12`
- 3 THALES  if he played in the current or last Thales Royale. This is all or nothing bonus.

## Configurable Variables
Configurable variables for this TIP:

- **max SNX Rewards Percentage** - the extra percentage added to the base reward due to SNX staking (e.g., max 15% added due to SNX staking).
- **max SNX Multiplier** - constant multiplier used to maintain the base rewards to SNX staking ratio (e.g., max extra rewards for stakers with *SNX staking >= multiplier x base reward*; )
- **max AMM Volume Rewards Percentage** - the extra percentage added to the base reward due to AMM volume (e.g., max 12% added due to produced AMM volume in the last 4 epochs).
- **max AMM Multiplier** - constant multiplier used to maintain the base rewards to AMM volume ratio (e.g., max extra rewards for stakers with *AMM volume >= multiplier x base reward*; )
- **max Thales Royale Participation Rewards Percentage** - the extra percentage added to the base reward due to Thales Royale participation (e.g., max 3% for Thales Royale participation in last and current season).

## Implementation
https://github.com/thales-markets/contracts/blob/main/contracts/EscrowAndStaking/StakingThales.sol

## Copyright
 
Copyright and related rights waived via CC0.
