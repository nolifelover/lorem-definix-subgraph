# Definix Subgraph

[Definix](https://bsc.definix.com/) is a decentralized protocol for automated token exchange on Binance Smart Chain.

This subgraph dynamically tracks any pair created by the uniswap factory. It tracks of the current state of Definix contracts, and contains derived stats for things like historical data and USD prices.

- aggregated data across pairs and tokens,
- data on individual pairs and tokens,
- data on transactions
- data on liquidity providers
- historical data on Definix, pairs or tokens, aggregated by day

## Running Locally

Make sure to update package.json settings to point to your own graph account.

## Queries

Below are a few ways to show how to query the uniswap-subgraph for data. The queries show most of the information that is queryable, but there are many other filtering options that can be used, just check out the [querying api](https://thegraph.com/docs/graphql-api). These queries can be used locally or in The Graph Explorer playground.

## Key Entity Overviews

#### UniswapFactory

Contains data across all of Definix v2. This entity tracks important things like total liquidity (in ETH and USD, see below), all time volume, transaction count, number of pairs and more.

#### Token

Contains data on a specific token. This token specific data is aggregated across all pairs, and is updated whenever there is a transaction involving that token.

#### Pair

Contains data on a specific pair.

#### Transaction

Every transaction on Definix is stored. Each transaction contains an array of mints, burns, and swaps that occured within it.

#### Mint, Burn, Swap

These contain specifc information about a transaction. Things like which pair triggered the transaction, amounts, sender, recipient, and more. Each is linked to a parent Transaction entity.

## Example Queries

### Querying Aggregated Definix Data

This query fetches aggregated data from all Definix pairs and tokens, to capture activity throughout the entire protocol.

```graphql
{
  uniswapFactories(first: 1) {
    pairCount
    totalVolumeUSD
    totalLiquidityUSD
  }
}
```

### Deployment
```
yarn codegen
graph codegen && graph build
graph deploy --product hosted-service nolifelover/definixexchange --strictNullChecks=false
```

###

Error
Handler skipped due to execution failure, error: Mapping aborted at ~lib/@graphprotocol/graph-ts/chain/ethereum.ts, line 448, column 6, with message: Call reverted, probably because an `assert` or `require` in the contract failed, consider using `try_getPair` to handle this in the mapping. wasm backtrace: 
0: 0x1e58 - <unknown>!~lib/@graphprotocol/graph-ts/chain/ethereum/ethereum.SmartContract#call 
1: 0x27a3 - <unknown>!src/types/templates/Pair/Factory/Factory#getPair 
2: 0x27f5 - <unknown>!src/mappings/pricing/findEthPerToken 
3: 0x2b05 - <unknown>!src/mappings/core/handleSync , handler: handleSync, block_hash: 0x5799c5d7596178294f8ece366d33032cc342ef2e04460bcdcf7eedc3b5d8db92, block_number: 6252460


Subgraph instance failed to run: Mapping aborted at ~lib/@graphprotocol/graph-ts/chain/ethereum.ts, line 448, column 6, with message: Call reverted, probably because an `assert` or `require` in the contract failed, consider using `try_getPair` to handle this in the mapping. wasm backtrace: 
0: 0x1e58 - <unknown>!~lib/@graphprotocol/graph-ts/chain/ethereum/ethereum.SmartContract#call 
1: 0x27a3 - <unknown>!src/types/templates/Pair/Factory/Factory#getPair 
2: 0x27f5 - <unknown>!src/mappings/pricing/findEthPerToken 
3: 0x2b05 - <unknown>!src/mappings/core/handleSync in handler `handleSync` at block #6252460 (5799c5d7596178294f8ece366d33032cc342ef2e04460bcdcf7eedc3b5d8db92), code: SubgraphSyncingFailure