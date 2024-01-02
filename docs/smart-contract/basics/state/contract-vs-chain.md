---
sidebar_position: 3
---

# Contract State vs. Chain State

The previous discussion was only about Contract States, which can be defined and used by developers themselves in the contract.

In the process of writing the aelf contract, it is very likely that the State on the aelf blockchain will also be needed. These states may arise from consensus and cross-chain mechanisms, or from the System Contracts of aelf.

These Chain States can be accessed through `Context` when you implementing contract methods. Of course, these states (context) are **read-only**.

For example, you can obtain current block height through `Context.CurrentHeight`, and obtain the id of executing transaction through `Context.TransactionId`. The complete apis will be listed in the next section.
