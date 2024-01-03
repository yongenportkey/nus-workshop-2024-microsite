---
sidebar_position: 1
---

# What is State

Blockchain is a state transition system where an initial state in combination with a transaction has a new state as an output. The process of executing a transaction is actually the execution of a method implemented in the contract.

<center>

```plantuml
@startuml

state HelloWorldContractState1 {
  state "Contract State" as cs1
  cs1: Counter = 0
}

state HelloWorldContractState2 {
  state "Contract State" as cs2
  cs2: Counter = 1
}

state HelloWorldContractState3 {
  state "Contract State" as cs3
  cs3: Counter = 2
}

[*] -> HelloWorldContractState1
HelloWorldContractState1: Block Height: 100
HelloWorldContractState1: Contract Method: Counter++
HelloWorldContractState1 --> HelloWorldContractState2: transaction (execute method)

HelloWorldContractState2 --> HelloWorldContractState3: transaction (execute method)
HelloWorldContractState2: Block Height: 101
HelloWorldContractState2: Contract Method: Counter++

HelloWorldContractState3: Block Height: 102
HelloWorldContractState3: Contract Method: Counter++
@enduml
```

</center>

As shown in the above figure, we have a HelloWorld Contract that has a State called Counter. The logic for modifying the Counter state is defined in the Contract Method, and as the transaction calling this method is executed, the Counter's state also changes as the block height grows.

Once the implementation of Contract Method is updated (this can happen on aelf through an UpdateSmartContract transaction), the logic for modifying the Counter state changes when the method is called again through a transaction.

<center>

```plantuml
@startuml

state HelloWorldContractState1 {
  state "Contract State" as cs1
  cs1: Counter = 0
}

state HelloWorldContractState2 {
  state "Contract State" as cs2
  cs2: Counter = 1
}

state HelloWorldContractState3 {
  state "Contract State" as cs3
  cs3: Counter = 2
}

state HelloWorldContractState4 {
  state "Contract State" as cs4
  cs4: Counter = 2
}

state HelloWorldContractState5 {
  state "Contract State" as cs5
  cs5: Counter = 4
}

[*] -> HelloWorldContractState1
HelloWorldContractState1: Block Height: 100
HelloWorldContractState1: Contract Method: Counter++
HelloWorldContractState1 --> HelloWorldContractState2: transaction (execute method)

HelloWorldContractState2 --> HelloWorldContractState3: transaction (execute method)
HelloWorldContractState2: Block Height: 101
HelloWorldContractState2: Contract Method: Counter++

HelloWorldContractState3: Block Height: 102
HelloWorldContractState3: Contract Method: Counter++
HelloWorldContractState3 --> HelloWorldContractState4: transaction (update HelloWorld Contract)

HelloWorldContractState4: Block Height: 103
HelloWorldContractState4: Contract Method: Counter+=2
HelloWorldContractState4 --> HelloWorldContractState5: transaction (execute method)

HelloWorldContractState5: Block Height: 104
HelloWorldContractState5: Contract Method: Counter+=2
@enduml
```

</center>

Therefore, it can be said that the code logic in the contract is mainly aimed at achieving one purpose: to inform the blockchain of how the state should be changed.

And these states happen to be defined within the contract. We also need to operate these states within the contract that defined the states.
