---
sidebar_position: 2
---

# Create a new project

## 1. Create project folder

At the Terminal, run the following commands:

```bash
mkdir workshop
cd workshop
dotnet new aelf -n Workshop
```

Open the `workshop` folder in your IDE.

## 2. Generated code

If you open your project folder, you should see two newly generated directories: src and test. These correspond to the smart contract code and the unit test code for the contract, respectively.

```bash
.
├── src
│   ├── Protobuf
│   │   ├── contract
│   │   │   └── hello_world_contract.proto
│   │   └── message
│   │       └── authority_info.proto
│   ├── Workshop.cs
│   ├── Workshop.csproj
│   └── WorkshopState.cs
└── test
    ├── Protobuf
    │   ├── message
    │   │   └── authority_info.proto
    │   └── stub
    │       └── hello_world_contract.proto
    ├── Workshop.Tests.csproj
    ├── WorkshopTests.cs
    └── _Setup.cs
```

## 3. Testing the code builds correctly

Before we start, let us check that the code builds correctly:

Run the commands:

```bash
cd src
dotnet build
# MSBuild version 17.6.8+c70978d4d for .NET
#   Determining projects to restore...
#   Restored .../src/Workshop.csproj (in 402 ms).
#   Workshop -> .../src/bin/Debug/net6.0/Workshop.dll
#   [CONTRACT-PATCHER] Saving as .../src/bin/Debug/net6.0/Workshop.dll.patched

# Build succeeded.
#     0 Warning(s)
#     0 Error(s)

# Time Elapsed 00:00:04.62
```
