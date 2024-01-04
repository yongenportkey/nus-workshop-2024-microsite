---
sidebar_position: 4
---

# Smart contract

## Introduction

The core of blockchain platforms can be viewed as a distributed multi-tenant database that stores the status of all the smart contracts deployed on it. Once deployed, each smart contract will have its unique address. The address will be used to query the execution status of the contract and can work as an identifier for status queries and updates. The contract code defines the details of these and updates, to be specific, how to check whether an account has permission to operate them and how the operation is completed.


## What makes a smart contract?
### The state
```CSharp
public class SimpleContractState : AElf.Sdk.CSharp.State.ContractState 
{
    // A state that holds string value
    public StringState Message { get; set; }
}
```
### Writing to the State
```CSharp
public override Empty Update(StringValue input)
{
    // Set the message value in the contract state
    State.Message.Value = input.Value;
    // Emit an event to notify listeners about something happened during the execution of this method
    Context.Fire(new UpdatedMessage
    {
        Value = input.Value
    });
    return new Empty();
}
```

### Reading the State
```CSharp
public override StringValue Read(Empty input)
{
    // Retrieve the value from the state
    var value = State.Message.Value;
    // Wrap the value in the return type
    return new StringValue
    {
        Value = value
    };
}
```

### The Interface
```protobuf
syntax = "proto3";

import "aelf/options.proto";
import "google/protobuf/empty.proto";
import "google/protobuf/wrappers.proto";
// The namespace of this class
option csharp_namespace = "AElf.Contracts.SimpleContract";

service SimpleContract {
  // The name of the state class the smart contract is going to use to access blockchain state
  option (aelf.csharp_state) = "AElf.Contracts.SimpleContract.SimpleContractState";

  // Actions (methods that modify contract state)
  // Stores the value in contract state
  rpc Update (google.protobuf.StringValue) returns (google.protobuf.Empty) {
  }

  // Views (methods that don't modify contract state)
  // Get the value stored from contract state
  rpc Read (google.protobuf.Empty) returns (google.protobuf.StringValue) {
    option (aelf.is_view) = true;
  }
}

// An event that will be emitted from contract method call
message UpdatedMessage {
  option (aelf.is_event) = true;
  string value = 1;
}
```

