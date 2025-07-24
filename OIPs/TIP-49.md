| id | Title | Status | Author | Description | Discussions to | Created |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |
| TIP-49 |  Account Merging | Vote Pending | Milkywave | Enable staked & vested thales account merging | https://discord.gg/WTe9sK5A | 2022-06-09



## Simple Summary
Make Account Merging always possible in order to enable transferring staked and vested Thales balances to a different account.

## Abstract 

To improve the UX, this TIP proposes that staked and vested Thales that are currently locked and can only be transferred after 7 days / 10 weeks, are to be made transferable. However, this TIP additionally proposes that the THALES transferred this way should also be staked and vested on the new receiving wallet.

## Motivation

Staked Thales are currently locked for 7 days (Cooldown) and Staking rewards are locked for 10 weeks from the date they are claimed, despite being locked they are still counted as staked. One of the consequences of this is that a staker who has earned rewards in a wallet is forced to continue to maintain this wallet. The purpose of locking these staking rewards was to ensure that they were not able to be transferred, however, this creates a problem if a wallet is compromised or if a user would like to cycle wallets. This TIP proposes a compromise whereby a staker can transfer the entire balance of their staked/vested balance to a different wallet.

Not being able to merge accounts has caused several problems to stakers, such as:
  
 - Small stakers foregoing rewards due to inability to consolidate large wallets. 
 - Less accounts staking as Thales is vested in wallets that are not maintained
 - Thales staker cannot benefit from bonus rewards as SNX was staked on another wallet
 - Overall worsening of UX
  
## Specification
A user will be able to sign a transaction assigning the Thales tokens in the staked/vested contract from the signing wallet to a new wallet. Only the full amount of Thales staked and vested will be able to be reassigned; partial reassignments will not be possible.

### Implementation
The Staking/RewardEscrow contract state will need to be migrated to a new staking/RewardEscrow with the added functionality of allowing users to reassign their staked/vested Thales reward balance between wallets that they control. It's completely self service.

1. Alice signs a transaction to reassign the staked/vested Thales token balance to a new wallet address she controls
2. Alice signs a transaction to accept the staked/vested Thales token balance reassignment at the new address.
3. Alice signs a transaction to confirm the staked/vested Thales token balance reassignment at the new address.


### Test Cases
SNX account merging [SIP-13](https://sips.synthetix.io/sips/sip-13/) and [SCCP-135](https://sips.synthetix.io/sccp/sccp-135/)


## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
