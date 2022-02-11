# Create New Token 



This is a  project for learning exploring blockchain runtime development with
[Substrate](https://substrate.dev/) and the
[FRAME](https://substrate.dev/docs/en/knowledgebase/runtime/frame). This
project implements a simple token creation and exchange protocol.

## Pallet Design Overview
### Calls
This pallet defines a simple token creation and transfer interface.
- `initialize_token(origin_id)`
- `transfer_token(from_id,to_id,amt)`

### Storages
-`Balances: StorageMap AccountId =>token_balance`

-`TotalSupply: StorageValue => u64`

### Events
- `Initialized(AccountId)`
- `TokenTransfered(from_id, to_id , amount)`

### Errors
-`AlreadyInitialized`

-`InsufficientFunds`

-`TokenOverflow`



## Build & Run

If you need to,
[set up your Substrate development environment](https://substrate.dev/docs/en/knowledgebase/getting-started/#manual-installation).
Then, build and run a development chain:

```shell
$ cargo run -- --dev --tmp
```

Once the node is running, use this link to open the Polkadot JS Apps UI and connect to the Substrate
node: https://polkadot.js.org/apps/#/settings/developer?rpc=ws://127.0.0.1:9944. Use the Settings >
Developer app and the contents of the [`types.json`](blob/master/types.json) file to add the
necessary types to the UI.


This project was forked from the
[Substrate Developer Hub Node Template](https://github.com/substrate-developer-hub/substrate-node-template).
