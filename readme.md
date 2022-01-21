# Smart Contract Verification

Etherscan compares the bytecode on the chain and the bytecode generated from
the provided source code match. Then they publish the source code, as
"verified"

The main purpose is to grantee the published source code is indeed the one
running on chain, so that everyone can audit the code, and evaluate the risk
before interacting with the smart contract.

So the verification doesn't serve as an audit, or security check. It's only the
first step

There are tools to perform security checks and static linting, such as:

[slither](https://github.com/trailofbits/slither) static analytic tool

[Echidna](https://github.com/trailofbits/echidna) property based fuzz tester

[eth-security-toolbox](https://github.com/trailofbits/eth-security-toolbox)
docker image that includes all the popular tools

## hacks

[Grim finance
hack](https://halborn.com/explained-the-grim-finance-hack-december-2021/)


# Upgradeable smart contract

[CN ref](https://juejin.cn/post/6844903685776998407)

[OpenZeppelin
Upgradeable](https://docs.openzeppelin.com/upgrades-plugins/1.x/)

## 原理

1. fallback() & delegatecall operator

2. "unstructured storage"

why it work: EVM storage is 256 bits to 256 bits key-value store

2*. Storage layout

instruction set: 256-bit operation, mload, mstore

[Reference](https://takenobu-hs.github.io/downloads/ethereum_evm_illustrated.pdf)


3. Transparency proxy vs UUPS proxy vs Beacon proxy

UUPS: Universal Upgradeable Proxy Standard (EIP1822). 

4. Tools: Truffle and hardhat upgradeable plugins

Compatibility validation on chain and offchain

## 注意事项

1. Replace `constructor` with `initialize`

2. Avoiding Initial Values in Field Declarations

3. Initializing the Implementation Contract

Always call the `initializer` modifier

4. Multiple Inheritance

Unlike constructor, initialize functions are not linearized by compiler, need
to manually organize to avoid calling the same init function multiple times.

5. No call to `selfdestruct` and `delegatecall`

