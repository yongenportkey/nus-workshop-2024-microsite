---
sidebar_position: 2
---

# Methods

The contract method not only tells the blockchain how to modify the States defined by this contract, but also includes other outputs. This section will discuss the inputs and outputs related to implementing contract methods.

**Inputs:**

- States defined by current contract
- States defined by other contracts
- States of aelf blockchain (Context)
- States of parent chain of side chains
  - This should be discussed in the aelf cross-chain mechanism
- Data from off-chain
  - This should be discussed in the oracle mechanism

**Outputs will be produced in the following situations:**

- States of current contract can be changed after transaction execution
- View methods are called so that other contracts can read states defined by current contract
- Events fired during the execution of transaction to inform subscriber

In addition, methods can also be called to each other through **inline transactions**. And actually, the only way to modify the States defined by other contracts is through inline transactions.

:::warning

It should be noted that **an inline transaction is not a real transaction**, it is only used to assist in completing the execution of the current transaction. And inline transactions can only be executed **after** the execution of the original transaction.

:::
