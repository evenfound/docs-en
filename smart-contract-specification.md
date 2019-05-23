## EVEN Network Smart Contracts Specification

### Overview

This is the specification document for the *smart contracts* (SC) required for the *Even Network*. It describes all types, variables, functions, their signatures, and their semantics.

### Definition

A *Even Smart Contract* (ESC) is a computer program library, whose functions can be executed inside a *Even Network Node* (ENN) process under control of the *Even Virtual Machine* (EVM). A contract consists of code (its functions) and data (its state) that resides at a specific address on the *Even DAG*.

### Principles and Goals

- **Security**: It should be possible and natural to build secure SM
- **Simplicity**: The language and the compiler implementation should strive to be simple
- **Auditability**: The contract code should be maximally human-readable. Furthermore, it should be maximally difficult to write misleading code. Simplicity for the reader is more important than simplicity for the writer, and simplicity for readers with low experience is particularly important

### Memory Model

A contract variable can be *state* or *temporary* variable.

- A contract’s *state variables* are the ones which define the contract’s state, are  permanently stored in contract storage and only changed by sendTransaction calls
- *Temporary variables* exist only inside the calling function (they cannot be declared outside of one). They get wiped after the function exits and they are generally cheaper to use than state variables

### Variables

Contract has access to a set of predefined variables:

- **even** — the global scope
- **msg** — represents current transaction
- **sender** — account that called the contract
- **value** — amount of tokens the user sent with the call

### Objects

Contract can create objects of following types:

- **wallet**
- **account**
- **transaction**

### Functions

A contract is actually just a library of functions. Only one function can be called in one invokation.

`default()`
A contract can also have a default function, which is executed on a call to the contract if no other functions match the given function identifier (or if none was supplied at all). The default function does not accept arguments and return values.

### API

| Namespace | Function | Parameters | Returns | Description |
|-----------|----------|------------|---------|-------------|
| **even**  | `wallet` | (name, password string) | name | Returns name of a wallet. The wallet may be in any state. New wallet should be generated before any use. The name is empty on failure. |
| **wallet** | `generate` | (name string) | seed-phrase string | Generates new HD wallet and returns the seed. The seed string is empty on failure. |
| **wallet** | `create` | (name, seed string) | seed-phrase string | Recreates HD wallet with known seed and returns the seed. The resulting string is empty on failure. |
| **wallet** | `nextaccount` | (name string) | account string | Generates next deterministic account. Returns address of new account on success or empty string otherwise. |
| **wallet** | `account` | (name, account string) | account string | Returns address of an account. The address is empty on failure (for instance, non-existent account). |
| **account** | `newtransaction` | (account string, tx-type int) | tx string | Returns address of a new transaction. This transaction should be properly initialized and published before any use. |
| **account** | `transaction` | (account, tx string) | tx string | Returns address of a transaction with known address or empty string on failure (for instance, non-existent transaction). |
| **transaction** | `save` | (tx string) | hash string | Publishes new transaction. Returns IPFS-hash of saved transaction on success or empty string otherwise (for instance, the transaction is already saved). |
