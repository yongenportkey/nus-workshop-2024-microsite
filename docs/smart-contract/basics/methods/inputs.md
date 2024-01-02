---
sidebar_position: 2
---

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Inputs

## 1. State types

The following are the currently supported state types that can be defined in the ContractState class:

<Tabs>
<TabItem value="SingletonState" label="SingletonState">

When you want to define a global unique value.

```csharp
public SingletonState<bool> IsInitialized { get; set; }
```

</TabItem>
<TabItem value="MappedState" label="MappedState">

When you want to define a mapping.

The mapping can be up to five levels.

```csharp
/// <summary>
/// Three levels:
/// User Address -> Token Symbol -> Balance
/// </summary>
public MappedState<Address, string, long> Balances { get; set; }
```

</TabItem>
<TabItem value="ContractReferenceState" label="ContractReferenceState">
  
When you want to call another contract or send inline transactions to another contract.

**The access level of this property must be `internal`**

```csharp
internal TokenContractContainer.TokenContractReferenceState TokenContract { get; set; }
```

</TabItem>
<TabItem value="ReadonlyState" label="ReadonlyState">
  
When you want to define a global unique value and this state can only be set value once.

```csharp
public ReadonlyState<string> NativeTokenSymbol { get; set; }
```

</TabItem>
</Tabs>

---

Besides, there are some other State types, but they are actually aliases of `SingletonState`.

| Alias                                        | Actual                                        |
| -------------------------------------------- | --------------------------------------------- |
| `BoolState`                                  | `SingletonState<bool>`                        |
| `Int32State`                                 | `SingletonState<int>`                         |
| `UInt32State`                                | `SingletonState<uint>`                        |
| `Int64State`                                 | `SingletonState<long>`                        |
| `UInt64State`                                | `SingletonState<ulong>`                       |
| `StringState`                                | `SingletonState<string>`                      |
| `BytesState`                                 | `SingletonState<byte[]>`                      |
| `ProtobufState<T> where T : IMessage, new()` | `SingletonState<T> where T : IMessage, new()` |

If you want to obtain the States defined by other contracts, you must call a View method provided by other contracts. If the corresponding State is not exposed through any View method, then there is no way.

## 2. Context

Also, inputs of a contract method including the following available context (Chain State):

| Chain State                 | Usage                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Context.ChainId             | Get current chain id.                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Context.CurrentHeight       | Get the block height when executing current transaction.                                                                                                                                                                                                                                                                                                                                                                                               |
| Context.CurrentBlockTime    | Get the block time when executing current transaction.                                                                                                                                                                                                                                                                                                                                                                                                 |
| Context.Self                | Get the address of current contract.                                                                                                                                                                                                                                                                                                                                                                                                                   |
| Context.Sender              | Get the sender address of executing transaction.                                                                                                                                                                                                                                                                                                                                                                                                       |
| Context.Origin              | Get the address of original transaction signer.                                                                                                                                                                                                                                                                                                                                                                                                        |
| Context.Transaction         | Get executing transaction.                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Context.PreviousBlockHash   | Get the block hash of previous block.                                                                                                                                                                                                                                                                                                                                                                                                                  |
| Context.TransactionId       | Get the TransactionId of the executing transaction.                                                                                                                                                                                                                                                                                                                                                                                                    |
| Context.OriginTransactionId | Get the TransactionId of the original transaction.                                                                                                                                                                                                                                                                                                                                                                                                     |
| Context.Variables           | Get variables configured during the launching of current chain. For example, on aelf MainChain:<ul><li>`Context.Variables.NativeSymbol` will return `ELF`</li><li>`Context.Variables.GetStringArray(AEDPoSContractConstants.PayTxFeeSymbolListName)` will return `{"WRITE","STORAGE","READ","TRAFFIC"}`</li><li>`Context.Variables.GetStringArray(AEDPoSContractConstants.PayRentalSymbolListName)` will return `{"CPU","RAM","DISK","NET"}`</li></ul> |

Additional explanation, as mentioned earlier, the method implementation of the contract is used to describe how the State should change, so class libraries unrelated to describing this logic are prohibited in the development process of the aelf contract. You can obtain restriction information from [this](https://docs.aelf.io/en/latest/architecture/smart-contract/restrictions/type.html) page.
