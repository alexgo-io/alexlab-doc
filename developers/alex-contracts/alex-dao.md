# ALEX DAO

## What is a DAO?

A DAO, or Decentralized Autonomous Organization, is a type of organization represented by rules encoded as a computer program that is transparent, and controlled by organization members. DAOs operate on blockchain technology, to automate and enforce rules and decisions without the need for a central authority.

## What is ALEX DAO?

ALEX DAO manages proposals to the ALEX platform which enables changes to be implemented in a rule-based way.

Changes to the platform can take various forms, including modifications to parameters, minting or burning of tokens, and adding, upgrading, or deprecating system contracts.

## ALEX DAO Architecture

<figure><img src="https://lh7-us.googleusercontent.com/docsz/AD_4nXf6vK4AOm5itG6jZRSN51-062TEUXy5pm_YGaubqMv-5cSDaAU8r4ddYu8pcwAjFdfyhljRIbKmAuCp-l6zJo1jgDJa1l3OHfpKc_Y1p0YYhoj_N2K7u9zlzxpPbzevwacLqx3hfufdG_keBvYZ9I4TtXHI?key=57qbJOwMTfP_p5xAvcRq3A" alt=""><figcaption></figcaption></figure>

### Main DAO Components Overview

This architecture has the following main components:

#### ALEX-DAO Contract

This is the core contract responsible for the DAO's operations and privileges. It is in charge of:

* Bootstrapping the DAO
* Defining new DAO features through extensions (modules)
* Executing proposals
* Authorizing components and extensions

#### Operators Contract

This contract manages the governance of the DAO and is implemented within ALEX's platform as an extension. It is responsible for:

* Managing and controlling the users with permission to propose and vote changes to the platform.
* Establishing proposal signaling thresholds
* Receive and hold presented proposals while being  voted/accepted
* Signaling (voting on) registered proposals
* Delegating proposal execution to the DAO operation contract
* Controlling the validity, resubmissions, and expirations of proposals

#### Extension Contracts

These individual contracts are designed to enhance the features and operations of the DAO by providing new specific implementations. These contracts usually have the same permissions as the DAO contract itself. (see is-dao-or-extension).

#### Proposal Contracts

Proposals are contracts that define updates to the DAO platform. They are meant to execute tasks reserved for the DAO's privileged executors (the ALEX DAO contract itself, or enabled extensions). These tasks can include platform state changes, executing actions, and introducing extensions to the platform. Each proposal is approved through a voting system implemented in the operator's extension. They are executed only once with the DAO contract as the transaction sender.

### Operations

### Proposals

_**Lifecyle**_

<figure><img src="https://lh7-us.googleusercontent.com/docsz/AD_4nXcMZZRgR7cp0tcwzXqIBgjPsaaOVe1n1gwtwFcAYhcy5CK_cRfyvUGAob6_6WER7OoZdgcO8OpsUBvXDFZL1ldp1ovD7Z_p8B5RsF8N30BGdJwqyZUENwk306BN_LpCe1H42k9HQ1Q3kqyR9UiCSli4FcLD?key=57qbJOwMTfP_p5xAvcRq3A" alt=""><figcaption></figcaption></figure>

_**Proposal created**_

A proposal is ready to be used when its contract is finally deployed.

_**New Proposal**_

Procedure to register the address of a given contract that conforms to the predefined proposal interface (trait).&#x20;

The operator that creates the proposal automatically signals 1 vote for it. Resubmissions (i.e. proposing again) are restricted only to non-executed expired proposals. This operation is restricted to enabled operators.

_**Signaling**_

Signaling is the process of voting for a certain registered and non-expired proposal in a boolean fashion (i.e., adding or subtracting 1 vote).&#x20;

Operators can only signal the same proposal twice if it has been resubmitted. The signaling procedure will trigger the execution step automatically if the proposal's signal count meets the threshold for execution. This operation is restricted to enabled operators.

_**Execution**_

As described in the signaling procedure, execution happens automatically when the signal count for the proposal meets the threshold.&#x20;

The procedure is delegated to the DAO operation contract, which restricts the operation to authorized extensions or the DAO contract itself. Finally, the execution invokes the proposal contract's execution method.

_**Expiration**_\
\
Proposal expiration occurs at a certain point in time (in the underlying burn blockchain) when the block height surpasses the validity period for that proposal.

The validity period is defined as the range of blocks from when the proposal was created until reaching the sum of that block plus a predefined delta (currently set to 144 blocks).

**Validation Logic**

Proposals have a validation status, which is accomplished if two conditions are met:

* The proposal has not expired.
* The proposal was created after the operator extension was set up, including any updates to operators or thresholds.

This validation is used in both new proposals and signaling procedures.

### Extensions

_**New extension**_

New extensions can be registered in the DAO core operation contract. This involves adding the address of a previously deployed contract, which will act as an administrative module of the DAO with privileges to execute core operations (e.g. adding new operators, updating thresholds or states, executing proposals, adding new extensions, etc.).

Only DAO operator members (i.e. the core contract alex-dao or previously registered and enabled extensions) can perform this step. Typically, new extensions are uno registered through proposal contracts when they receive a majority of votes.

_**Availability**_

During or after the registration of a module (extension), other DAO operator members can enable or disable the extension in a boolean fashion. Although disabled extensions will remain registered in the core contract, they will not be permitted to perform future operations while in that state.

As with the registration process, only DAO operator members have the authority to change the status of extensions.

_**Callbacks**_

Extensions that conform to the predefined extension interface (trait) have access to the core contract’s "Extension Requests" special feature. This feature allows other enabled extensions to call the core contract, which in turn, can call back the initiating extension to perform a specific callback method with alex-dao privileges. This includes the sender that triggered the call and a provided payload.

## Examples

### A proposal: agp-222.clar

The agp-222 contract is a proposal whose main purpose is to extend the DAO platform by attaching the AMM-Pool contract (a DAO platform extension) and performing a series of maintenance tasks on the DAO platform.

For it to be executed, it must first be accepted by the platform. The process is as follows:

* The extension (in this case, the amm-pool-v2-01 contract) is created along with this proposal contract.
* Once both contracts are created and deployed, the proposal is submitted to the DAO platform through the operators (extension) contract. This contract verifies that the submission is made by a DAO-operator.
* The proposal is then put to a vote by the remaining DAO-operators (it is assumed that the submitting operator votes in favor, and its vote is automatically counted with the submission).
* At some point, the proposal either reaches a predefined threshold or it expires. If the threshold is reached, the operators contract invokes the executor-dao contract to run the proposal's execute() code with DAO privileges. In this way, the code in the proposal gains the necessary permissions, allowing it to invoke any required DAO platform functionality as if it were already part of the DAO. This enables the proposal to do things like:
  * Include new extensions to the platform (as well as remove, stop, pause, etc.).
  * Reconfigure token pools.
  * Reconfigure blocklists.
  * Confirm special cases of token migrations.
  * Etc.
* After all actions by the proposal are executed, it is discarded and cannot execute its code again or regain DAO privileges.

#### In this particular case

As we mentioned before, in this particular case, the proposal performs two actions:

1. It extends the DAO platform(\*) by attaching the AMM-Pool contract (the extension deployed along with this proposal), making it ready to operate immediately.
2. It performs a series of maintenance tasks on the DAO platform.

To perform the extension attachment to the platform, a new invocation is made to the executor-dao contract, which is responsible for keeping track of which extensions are in use (and subsequently allowing anyone to check if an invoking contract is an approved extension).

The maintenance task included in this proposal, in this particular case, involves blocking a set of 89 abusive addresses to prevent their usage of the system.

<figure><img src="https://lh7-us.googleusercontent.com/docsz/AD_4nXeI08FmEbaM4dpKhV7DTDKZrwa4CK0qD3Io6J58T5AN2pxz6zQo-UCFCoiHPFP7GWc-UudcsbbZCWViZXOqRk3y0Z_Puv-W7ANnnCbSphwmWifWFqkPm7kWvJjucophcejHltOzYd8hHYmrwLM6SDk2DRc1?key=57qbJOwMTfP_p5xAvcRq3A" alt=""><figcaption></figcaption></figure>

(\*) DAO-platform = the DAO contracts or its extensions.

(\*\*) DAO-operator: a contract already part of the DAO-platform or a user of the system with operator privileges.

### An extension: The AMM-pool

The amm-pool-v2-01 contract is a platform extension that implements a token swap pool, focusing on the pool mechanics. In contrast, the auxiliary contract amm-registry-v2-01 acts as a pool registry. Here, each pool, along with its properties such as the pool owner's address, must be registered. This separation of concerns allows for a simple permission system, supporting privileged operations by certain actors.

Both mentioned contracts are extensions of the DAO-platform and are allowed to invoke each other with full permissions.

By design, the sensitive data (pool configuration, behavior, state, ownership, and other properties) is contained and ultimately managed by the registry contract. All operations in this registry contract require invocation by the DAO-platform.

On the other hand, the amm-pool extension contract includes governance calls for system reconfiguration. Authentication here is broader than in the registry, allowing not only the DAO platform but also pool owners (who may not necessarily be DAO platform members) to reconfigure pools. In the latter case, the amm-pool checks pool ownership by the invoker and, if applicable, uses its permissions as a member of the DAO platform to invoke reconfiguration functions in the registry.
