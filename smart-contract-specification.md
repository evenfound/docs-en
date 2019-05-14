# EVEN Network Smart Contracts Specification

## Overview

This is the specification document for the *smart contracts* (SC) required for the *Even Network*. It describes all types, variables, functions, their signatures, and their semantics.

## Definition

A *Even Smart Contract* (ESC) is a computer program library, whose functions can be executed inside a *Even Network Node* (ENN) process under control of the *Even Virtual Machine* (EVM). A contract consists of code (its functions) and data (its state) that resides at a specific address on the *Even DAG*.

## Principles and Goals

- **Security**: It should be possible and natural to build secure SM
- **Simplicity**: The language and the compiler implementation should strive to be simple
- **Auditability**: The contract code should be maximally human-readable. Furthermore, it should be maximally difficult to write misleading code. Simplicity for the reader is more important than simplicity for the writer, and simplicity for readers with low experience is particularly important

## Memory Model

A contract variable can be *state* or *temporary* variable.

- A contract’s *state variables* are the ones which define the contract’s state, are  permanently stored in contract storage and only changed by sendTransaction calls
- *Temporary variables* exist only inside the calling function (they cannot be declared outside of one). They get wiped after the function exits and they are generally cheaper to use than state variables

## Variables

Contract has access to a set of predefined variables:

- **even** — the global scope
- **msg** — represents current transaction
- **sender** — account that called the contract
- **value** — amount of tokens the user sent with the call

## Objects

Contract can create objects of following types:

- **Wallet** {seed}
- **Account** {privateKey, publicKey}
- **Transaction** {sender, receiver, value}

## Functions

`even.hash(message)`
Hashes the given message and returns the hash.

`even.sign(message, privateKey)`
Signs arbitrary data and returns the signature.

`even.verify(message,signature,publicKey)`
Signs arbitrary data.

`even.createStorage(key)`
Creates a storage (persistent) variable.

`even.wallet(name, password)`
Creates and returns a wallet object (not wallet itself).

`wallet.generate()`
Creates a brand-new, unique encrypted wallet. Returns new seed mnemonic phrase.

`wallet.create(seed)`
(Re)creates encrypted wallet with known seed.

`wallet.unlock()`
Unlocks the wallet temporarily.

`wallet.account()`
Creates and returns an account object.

`account.next()`
Generates next deterministic account. Returns the new account’s address.

`account.balance()`
Returns current balance of the account.

`account.address()`
Returns the account’s address.

`account.privateKey()`
Returns the account’s private key.

`account.publicKey()`
Returns the account’s public key.

`account.createTransaction(address)`
Creates a transaction object with the sender address.

`tx.sign(privateKey)`
Signs a transaction with a given private key.

`tx.send()`
Sends a transaction.

`default()`
A contract can also have a default function, which is executed on a call to the contract if no other functions match the given function identifier (or if none was supplied at all). The default function does not accept arguments and return values.
