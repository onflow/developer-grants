# Flow Reference Wallet - On Chain Recovery

# Description

A user may wish to configure their account with an on-chain recovery mechanism in order to regain access to their account in the event they lose access to one of their account keys. 

There should be many varying types of on-chain account recovery mechanisms that exist. These mechanisms should have their own individual logic for how they facilitate account recovery. 

For example, recovery mechanics could be, but are not limited to:

- Allow a user to configure a new key on their account if the account’s Flow balance falls below a set amount.
- Allow a user to configure a new key on their account if a predefined group of other accounts successfully vote to configure a new key on the account.
- Allow a user to configure a new key on their account if the account has not signed a transaction for a specified number of blocks.

A user should choose which account recovery mechanisms they may wish to enable on their account. The chosen account recovery mechanisms should be invocable from within the users wallet. All recovery mechanisms should conform to the same interface so they can be executed consistently. 

As an example, here is a possible on-chain interface that each on-chain recovery mechanic could implement:

https://github.com/JeffreyDoyle/flow-account-recovery/blob/main/cadence/contracts/account-recovery.cdc#L1-L8

Every recovery mechanism would implement the interface, and the specified recover method. The recovery method consumes a new key to configure on the account, along with an opaque data parameter which allows the method to consume additional data required to perform its specific recovery mechanic. Each recovery mechanism could implement additional methods beyond those specified in the interface to help them perform their individual mechanics.

Here is a toy example of a base-case account recovery mechanism, which configures a new key on the account:  

https://github.com/JeffreyDoyle/flow-account-recovery/blob/main/cadence/contracts/basic-account-recovery.cdc

This toy example would be undesirable to use in practice as it does not require any condition to be met for the new key to be set on the account.

## Integration

The on-chain account recovery framework will need to be created, along with several on-chain account mechanisms that implement a variety of account recovery possibilities.

Flow Core Wallet will need to use the on-chain account recovery framework to allow users to configure their account with their desired account recovery mechanisms. Users will need to be able to perform account recovery if the conditions for their account recovery mechanisms are met within Flow Core Wallet.

## Impact

On-chain recovery mechanisms will promote safer self-custody of user assets on Flow. By providing a framework for developers to build their own account on-chain recovery mechanisms, that all implement a shared interface, users can choose their desired account recovery mechanisms to configure their account with all within their wallet.

# Grant Application

To apply for a developer grant to be compensated for addressing this project, follow the existing grant applicatin process and reference this project in your application. 
