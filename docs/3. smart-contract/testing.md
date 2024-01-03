---
sidebar_position: 4
---

# Testing

## 1. Test template code

At the Terminal, run the following commands:

```bash
cd test
dotnet test
```

## 2. Modify test cases

For any changes made to protobuf in the `src` folder, similar modifications should be applied to protobuf in the test
folder. Modify the `test/HelloWorldTests.cs` file to create new test cases for testing the newly written code logic.
