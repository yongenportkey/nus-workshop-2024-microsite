---
sidebar_position: 3
---

# Modify the generated code

First, open the folder in your IDE.

Edit the following files:

## src/Protobuf/contract/hello_world_contract.proto

In this file,

```protobuf
syntax = "proto3";

import "aelf/options.proto";
import "google/protobuf/empty.proto";
import "google/protobuf/wrappers.proto";
// The namespace of this class
option csharp_namespace = "AElf.Contracts.Workshop";

service Workshop {
  // The name of the state class the smart contract is going to use to access blockchain state
  option (aelf.csharp_state) = "AElf.Contracts.Workshop.WorkshopState";

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

## src/Workshop.cs

```csharp
using AElf.Sdk.CSharp;
using Google.Protobuf.WellKnownTypes;

namespace AElf.Contracts.Workshop
{
    // Contract class must inherit the base class generated from the proto file
    public class Workshop : WorkshopContainer.WorkshopBase
    {
        // A method that modifies the contract state
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

        // A method that read the contract state
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
    }

}
```
