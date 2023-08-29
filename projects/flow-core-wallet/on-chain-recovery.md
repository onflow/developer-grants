# Flow Core Wallet - On Chain Recovery

# Description

A user may wish to configure their account with an on-chain recovery mechanism in order to regain access to their account in the event they lose access to one of their account keys. 

There should be the possibility for many varying types of account recovery mechanisms to exist. These mechanisms should have their own individual logic for how they facilitate account recovery. For example, a recovery mechanic could be, but are not limited to:

- Allow a user to set a new key to an account if the account’s Flow balance falls below a set amount.
- Allow a user to set a new key to an account if a set group of authorized accounts successfully vote to set a new key to the account.
- Allow a user to set a new key to an account if the account has not signed a transaction for a specified number of blocks.

A user of Flow Core Wallet should choose which account recovery mechanism they may wish to configure their account with, and that account recovery mechanism should be invocable from within Flow Core Wallet. All recovery mechanisms should conform to the same interface so they can consistently be executed. As an example, here is an example interface that could work:

https://github.com/JeffreyDoyle/flow-account-recovery/blob/main/cadence/contracts/account-recovery.cdc#L1-L8

In this case, every recovery mechanism would implement the interface and the recover method. The recovery method consumes a new key to set on the account, along with an opaque data parameter which allows the method to consume additional data required to perform its recovery mechanic. To facilitate the recovery mechanic, the recovery mechanism could additionally implement other methods.

Here is an example of a base case recovery mechanism, which sets a new key on the account:  

https://github.com/JeffreyDoyle/flow-account-recovery/blob/main/cadence/contracts/basic-account-recovery.cdc

This toy example would be undesirable to use in practice as it does not require any condition to be met for the new key to be set on the account.

## Integration

Flow Core Wallet will need to use the on-chain account recovery mechanism framework to allow users to configure their account with their desired account recovery mechanism, and execute account recovery if the conditions for the mechanism are met within the Flow Core Wallet UI.

## Impact

On-chain recovery mechanisms promote safer self-custody options for account management on blockchain. By providing a framework for developers to build their own account recovery mechanics on-chain, that leverage a shared interface, users can choose their desired account recovery mechanisms to configure their account with. 

# Grant Application

To apply for a developer grant to be compensated for addressing this project, follow the existing grant applicatin process and reference this fea
