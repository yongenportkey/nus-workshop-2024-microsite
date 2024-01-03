---
sidebar_position: 3
---

# Modify the generated code

The next step in development would be to modify the code for the smart contract.

Clone the code at https://github.com/yongenportkey/aelf-nus-workshop-2024 and open the folder in your IDE.

```bash
git clone https://github.com/yongenportkey/aelf-nus-workshop-2024
cd aelf-nus-workshop-2024
cd contract
code .
```

This will serve as a quick starting point for the remainder of the workshop.

You should see these files under the contract folder:

```bash
contract
├── POAPContract
│   ├── src
│   │   ├── ContractsReferences.cs
│   │   ├── POAPContract.cs
│   │   ├── POAPContract.csproj
│   │   ├── POAPContractState.cs
│   │   └── Protobuf
│   │       ├── contract
│   │       │   └── poap_contract.proto
│   │       ├── message
│   │       │   └── authority_info.proto
│   │       └── reference
│   │           └── token_contract.proto
│   └── test
│       ├── POAPContract.Tests.csproj
│       ├── POAPContractTests.cs
│       ├── Protobuf
│       │   ├── message
│       │   │   └── authority_info.proto
│       │   └── stub
│       │       ├── acs0.proto
│       │       ├── poap_contract.proto
│       │       └── token_contract.proto
│       └── _Setup.cs
├── POAPContract.sln
├── src
│   ├── ContractsReferences.cs
│   ├── POAPContract.cs
│   ├── POAPContract.csproj
│   ├── POAPContractState.cs
│   └── Protobuf
│       ├── contract
│       │   └── poap_contract.proto
│       ├── message
│       │   └── authority_info.proto
│       └── reference
│           └── token_contract.proto
└── test
    ├── POAPContract.Tests.csproj
    ├── POAPContractTests.cs
    ├── Protobuf
    │   ├── message
    │   │   └── authority_info.proto
    │   └── stub
    │       ├── acs0.proto
    │       ├── poap_contract.proto
    │       └── token_contract.proto
    └── _Setup.cs
```
