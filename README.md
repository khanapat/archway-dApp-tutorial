# archway-dApp-tutorial

Archway is a smart contract platform which gives developers the tools to quickly build and launch scalable cross-chain dApps.

The network starts with a vanilla Proof-of-Stake (PoS) network, with modified Minting, CosmWasm, Distribution, Staking, Group, and Governance Cosmos modules that manage the Archway inflation and rewards system.

Smart Contract in archway protocal uses CosmWasm, WebAssembly(Wasm), and Rust.

This tutorial is to build and deploy smart contract in archway

## Installation

- [Rustc](https://www.rust-lang.org/tools/install)
- [Cargo](https://doc.rust-lang.org/cargo/getting-started/installation.html)
- [Archwayd](https://github.com/archway-network/archway/tree/main/cmd/archwayd)
- [Archway Developer CLI](https://github.com/archway-network/archway-cli)

## Setup

Let's setup a new project, using Archway Developer CLI.

### Creating an account

To create a new wallet

```sh
archway accounts --add <account-name>
```

> **_NOTE:_** when got error: no such subcommand: run-script. Using `cargo install cargo-run-script` to install run-script.

### Query account balance

To check account balance

```sh
archwayd query bank balances <account-address> --node <rpc-host>:<rpc-port> --chain-id <network-id>
```

### Requesting Testnet funds

To request funds from the faucet you should use our Discord channel.

1. Join our Discord server at https://discord.gg/dnYYcKPAX5
2. Send the following message in the 🚰 ｜ faucet channel

```sh
!faucet <address>
```

The funds will be deposited to your account in a few minutes on all testnets.

## Creating first dApp

Let's create first dApp project, using Archway Developer CLI.

### Creating a new project

To create a project with template.

```sh
archway new
```

### Deploy a smart contract

Default wasm executables can be produced by the developer CLI using the command.

To deploy a smart contract

```sh
archway deploy --args '<arguments>'
```

### Interact with smart contract

- Querying - Queries read from the blockchain. They don't modify anything stored on chain, so they don't cost a fee.

```sh
archwayd query wasm contract-state smart <contract-address> <query> --node <rpc:443> --chain-id <chain-id>
```

- Execute - Transactions write to the blockchain and cost a gas fee for modifying a contract's state securely.

```sh
archway tx --args '<arguments>'
or
archwayd tx wasm execute <contract-address> '<arguments>' --node <rpc:443> --chain-id <chain-id> --from <account-address>
```

## Creating NFT

Let's create nft project, using Archway Developer CLI.

### Deploy a smart contract

The contract instantiation requires three parameters:

1. name (the NFT collection name)
2. symbol (a token symbol to represent it)
3. minter (the wallet address allowed to mint a new NFT using this contract)

```sh
archway deploy --args '{ "name": <name>, "symbol": <symbol>, "minter": <account> }'
```

### Interact with smart contract

- Minting - mint an NFT with MintMsg parameters

```sh
archway tx --args '{"mint":{"token_id":"<token-id>","owner":<account-address>,"extension":{"name":"<name>","description":"<description>","image":"<image-url>","attributes":[{"trait_type":"<trait-type>","value":"<value>"}]}}}'
```

- Querying - get nft infomation

```sh
archwayd query wasm contract-state smart <contract-address> '{"nft_info":{"token_id":"<token-id>"}}' --node <rpc:443> --chain-id <chain-id>

archwayd query wasm contract-state smart <contract-address> '{"owner_of":{"token_id":"<token-id>"}}' --node <rpc:443> --chain-id <chain-id>
```

- Sending - transfer nft token

```sh
archway tx --args '{"transfer_nft":{"recipient":"<account-address>","token_id":"<token-id>"}}'
```
