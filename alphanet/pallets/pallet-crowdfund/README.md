# Simple Crowdfund Pallet



This is a  project for learning exploring blockchain runtime development with
[Substrate](https://substrate.dev/) and the
[FRAME](https://substrate.dev/docs/en/knowledgebase/runtime/frame). This
project implements a simple crowdfund pallet.

## Crowdfunding Pallet Design Overview
### Calls
This pallet defines a simple crowdfunding application interface throw which user can interact and contribute
- `create(origin, beneficiary, goal, end)`
- `contribute(origin,index,value)`
- `withdraw(origin,index)`
- `dissolve(origin, index)`
- `dispense(origin, index)`

### Data Structure
```rust
pub struct FundInfo<AccountId, Balance, BlockNumber> {
  pub beneficiary:      AccountId,
  pub deposit:          Balance,
  pub raised:           Balance,
  pub end:              BlockNumber,
  pub goal:             Balance
}
```

```rust
type FundIndex = u32;
type AccountIdOf<T> = <T as frame_system::Config>::AccountId;
type BalanceOf<T> = << T as Config>::Currency as Currency<AccountIdOf<T>>>::Balance;
type FundInfoOf<T> = FundInfo<AccountIdOf<T>, BalanceOf<T>, <T as frame_system::Config>::BlockNumber>;
```

### Storages
-`funds: StorageMap FundIndex =>FundInfoOf`

-`fund_count: StorageValue => u32`

### Events
- `Created(FundIndex, T::BlockNumber)`
- `Contributed(T::AccountId, FundIndex, BalanceOf<T>, T::BlockNumber)`
- `Withdrew(T::AccountId, FundIndex, BalanceOf<T>, T::BlockNumber)`
- `Retiring(FundIndex, T::BlockNumber)`
- `Dissolved(FundIndex, T::BlockNumber, T::AccountId)`
- `Dispensed(FundIndex, T::BlockNumber, T::AccountId)`

### Errors
- `EndTooEarly`
- `ContributionTooSmall`
- `InvalidIndex`
- `ContributionPeriodOver`
- `FundStillActive`
- `NoContribution`
- `FundNotRetired`
- `UnsuccessfulFund`



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
