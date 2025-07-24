| id | Title | Status | Author | Description | Discussions to | Created |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| TIP-12 | Deploy Thales protocol on Optimism Mainnet | Implemented | Danijel (@dgornjakovic) | Deploy and enable the suite of contracts pertaining to Thales protocol on Optimism Mainnet | https://discord.gg/8bzFdpGTrp | 2021-12-10
 
## Simple Summary
 
This TIP proposes to deploy and support Thales protocol on Optimism Mainnet L2 chain.
 
## Abstract
 
This TIP proposes to deploy and support Thales protocol contracts to Optimism mainnet. With the rollout of OVM 2.0, Thales has been whitelist to deploy on Optimism Mainnet. Contracts have been tested and working on OVM and Thales project is now ready, from a technical standpoint, to support this L2 chain.  
This TIP also proposes to only whitelist Thales Protocol DAO for functionality of creating a market and to reduce minimal requirement for minting options tokens to 1 sUSD. The goal behind this decision is to support AMM contract deployment and to focus liquidity to a small number of markets deployed by the Protocol DAO.
 
## Motivation
 
MVP version of Thales was deployed on mainnet to showcase to the community at large what Thales is about. Gas prices on L1 have held Thales back to an extent, but we grew together as a protocol and community, learned some lessons which we have incorporated into the L2 rollout and we are now proposing to the council to formally deploy and enable Thales on Optimism Mainnet.
 
## Specification
 
This TIP entails Thales Protocol DAO to execute the following points:  

* Deploy the following contracts from the BinaryOptions suite to the Optimism Mainnet:  

    * [BinaryOptionMarketFactory.sol](https://github.com/thales-markets/contracts/blob/main/contracts/BinaryOptions/BinaryOptionMarketFactory.sol)
    * [BinaryOptionMarketManager.sol](https://github.com/thales-markets/contracts/blob/main/contracts/BinaryOptions/BinaryOptionMarketManager.sol)
    * [BinaryOptionMarketData.sol](https://github.com/thales-markets/contracts/blob/main/contracts/BinaryOptions/BinaryOptionMarketData.sol)
    * [BinaryOptionMarketMastercopy.sol](https://github.com/thales-markets/contracts/blob/main/contracts/BinaryOptions/BinaryOptionMarketMastercopy.sol)
    * [BinaryOptionMastercopy.sol](https://github.com/thales-markets/contracts/blob/main/contracts/BinaryOptions/BinaryOptionMastercopy.sol)
      
These contracts are also deployed on L1, but now also include the following changes: 
 - Changes introduced with TIP-8
 - `burn` function introduced with the ThalesAMM (TIP-11)
 - Whitelist market creation exclusively to Thales Core Contributors addresses
 - Reduce minimal required amount of sUSD for minting options tokens to be `1`
    
* Deploy the Thales PriceFeed proxy that will serve asset prices from Chainlink for resolving markets:
    * [PriceFeed.sol](https://github.com/thales-markets/contracts/blob/main/contracts/PriceFeed/PriceFeed.sol)  
    
Thales was using Synthetix ExchangeRates contract for the MVP, but as Thales can expand its offering beyond assets that are synths, it will now has its own contract to serve as a wrapper over Chainlink Price aggegator feeds. PriceFeed.sol can also be expanded to support a TWAP feed from UniV3 on Optimism.

* Deploy Thales AMM contract to support out of the box liquidity on Thales markets:

    * [ThalesAMM.sol](https://github.com/thales-markets/contracts/blob/ThalesAMM/contracts/AMM/ThalesAMM.sol)
    * [DeciMath.sol](https://github.com/thales-markets/contracts/blob/ThalesAMM/contracts/AMM/DeciMath.sol) (helper contract for Math operations]

* Deploy Thales Royale contract with seasons and buy-ins (more details in a dedicated TIP):
    * [ThalesRoyale.sol](https://github.com/thales-markets/contracts/blob/ThalesAMM/contracts/ThalesRoyale/ThalesRoyale.sol) 

* Add support in the thalesmarket.io dapp for Optimism L2 with limit orders backed by 1inch protocol.
    * Include 1inch integration to buy sUSD directly from the dapp

Thales integrated 0x protocol into L1 MVP. However, post whitelisting on Optimism Thales could not get enough certainty around 0x API being made available on Optimism, so this TIP proposes to rollout with 1inch limit orders API, and keep the option to revert back to 0x or even support both protocols once 0x API is ready.  

## Rationale
TBD
 
## Test Cases
N/A
## Implementation
N/A 
## Copyright
 
Copyright and related rights waived via CC0.
