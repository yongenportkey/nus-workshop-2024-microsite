---
sidebar_position: 1
---

# Changed States

As mentioned earlier, the States defined in the contract must be modified through transactions. The truth is, when a method that involves modifying a State (directly assign a value to State) is executed in the form of a transaction, it generates a `TransactionExecutingStateSet` instance. This protobuf type is defined in `aelf/core.proto`.

```protobuf
message TransactionExecutingStateSet {
    // The changed states.
    map<string, bytes> writes = 1;
    // The read states.
    map<string, bool> reads = 2;
    // The deleted states.
    map<string, bool> deletes = 3;
}
```

No matter what actions you take in the corresponding state, such as reading, writing, or deleting, they will be recorded in the `TransactionExecutingStateSet` instance. Subsequently, these records will be written into blockchain as the transaction is packaged into the block, allowing the State to be truly modified.
