---
title: Deploy contract using AELF Explorer
sidebar_position: 1
---

Deployment on AElf test net is very simple, it can be done on the website: https://explorer-test-side02.aelf.io/

Deployment procedure:

1. Implement acs12.proto

We need create a new file called `acs12.proto` under `src/Protobuf/reference` folder, this is a standard aelf package for showing users gas fee. `Acs12.proto` is necessary for deployment on AElf test net.
We can also download `acs12.proto` from [here](https://github.com/AElfProject/AElf/blob/dev/protobuf/acs12.proto).

```protobuf copy
/**
 * AElf Standards ACS12(User Contract Standard)
 *
 * Used to manage user contract.
 */
syntax = "proto3";

package acs12;

import public "aelf/options.proto";
import public "google/protobuf/empty.proto";
import public "google/protobuf/wrappers.proto";
import "aelf/core.proto";

option (aelf.identity) = "acs12";
option csharp_namespace = "AElf.Standards.ACS12";

service UserContract{

}

//Specified method fee for user contract.
message UserContractMethodFees {
  // List of fees to be charged.
  repeated UserContractMethodFee fees = 2;
  // Optional based on the implementation of SetConfiguration method.
  bool is_size_fee_free = 3;
}

message UserContractMethodFee {
  // The token symbol of the method fee.
  string symbol = 1;
  // The amount of fees to be charged.
  int64 basic_fee = 2;
}
```

Then we can add implementation to `poap_contract.proto`

```protobuf copy
syntax = "proto3";

import "aelf/core.proto";
import "aelf/options.proto";
import "google/protobuf/empty.proto";
import "google/protobuf/timestamp.proto";
// highlight-next-line
import "Protobuf/reference/acs12.proto";
// The namespace of this class
option csharp_namespace = "AElf.Contracts.POAPContract";

service POAPContract {
  // The name of the state class the smart contract is going to use to access blockchain state
  option (aelf.csharp_state) = "AElf.Contracts.POAPContract.POAPContractState";
  // highlight-next-line
  option (aelf.base) = "Protobuf/reference/acs12.proto";

  rpc Initialize (google.protobuf.Empty) returns (google.protobuf.Empty) {
  }
  rpc CreateCollection (CreateCollectionInput) returns (google.protobuf.Empty) {
  }
  rpc Mint (google.protobuf.Empty) returns (google.protobuf.Empty) {
  }
}

message Minted {
  option (aelf.is_event) = true;
  string symbol = 1;
  aelf.Address receiver = 2;
}

message CreateCollectionInput {
  string symbol = 1;
  string nft_image_url = 2;
  string event_title = 3;
  string event_date = 4;
  string event_venue = 5;
  string event_description = 6;
  google.protobuf.Timestamp event_start_time = 7;
  google.protobuf.Timestamp event_end_time = 8;
}

message CollectionInfo {
  string nft_image_url = 1;
  string event_title = 2;
  string event_date = 3;
  string event_venue = 4;
  string event_description = 5;
}
```

Then build under src folder again.

:::warning
Please note that the DLL contract files with identical code cannot be deployed repeatedly.
If you intend to deploy contract code with the same logic, make a slight modification in the code. For instance, add a line like `var name = "xxx"`.
:::

```bash copy
dotnet build
```


2. Go to https://explorer-test-side02.aelf.io/proposal/proposals and login your portkey account, and transfer some tokens to sidechain as we need deploy on sidechain.

If you haven't don't have test tokens on your account, you may go to https://testnet-faucet.aelf.io/ to get some free test tokens.

Here is how to tranfer test tokens to side chain:
![](/img/extension_sidechain.gif)

3. Submit a proposal

Click "Apply", and select "Deploy/Update Contract", upload the `/AElf.Contracts.HelloWorld.dll.patched` file in project folder

```bash copy
workshop/src/bin/Debug/net6.0
```

4. Deploy the contract

After uploading your contarct file, click "Apply" at bottom then click "OK" in pop-up window, it will do code check and deployment automatically.

:::warning
Please do not close the pop-up window until it's done, the address will be shown in pop-up window.
:::

Here is a gif of the whole deployment process.
![](/img/output.gif)
