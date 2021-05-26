# FeraSwap Subgraph

Aims to deliver analytics & historical data for FeraSwap. Still a work in progress. Feel free to contribute!

The Graph exposes a GraphQL endpoint to query the events and entities within the FeraSwap ecosytem.

Current subgraph locations:

1. **Exchange**: Includes all FeraSwap Exchange data with Price Data, Volume, Users, etc:
   + https://thegraph.com/explorer/subgraph/feraswap/exchange (mainnet)
   + https://thegraph.com/explorer/subgraph/feraswap/fantom-exchange (ftm)
   + https://thegraph.com/explorer/subgraph/feraswap/matic-exchange (matic)
   + https://thegraph.com/explorer/subgraph/feraswap/xdai-exchange (xdai)
   + https://thegraph.com/explorer/subgraph/feraswap/bsc-exchange (bsc)

2. **Master Chef**: Indexes all MasterChef staking data: https://thegraph.com/explorer/subgraph/feraswap/master-chef

3. **Fera Maker**: Indexes the FeraMaker contract, that handles the serving of exchange fees to the FeraBar: https://thegraph.com/explorer/subgraph/feraswap/fera-maker

4. **Fera Timelock**: Includes all of the timelock transactions queued, executed, and cancelled: https://thegraph.com/explorer/subgraph/feraswap/fera-timelock

5. **Fera Bar**: Indexes the FeraBar, includes data related to the bar: https://thegraph.com/explorer/subgraph/feraswap/fera-bar

6. **FeraSwap-SubGraph-Fork** (on uniswap-fork branch): Indexes the FeraSwap Factory, includes Price Data, Pricing, etc: https://thegraph.com/explorer/subgraph/jiro-ono/feraswap-v1-exchange

7. **BentoBox**: Indexes BentoBox and Kashi Lending data: https://thegraph.com/explorer/subgraph/feraswap/bentobox

8. **MiniChef**: Indexes MiniChef contracts that are used in place of MasterChefs for alternate networks:
  + https://thegraph.com/explorer/subgraph/feraswap/matic-minichef

## To setup and deploy

For any of the subgraphs: `feraswap` or `bar` as `[subgraph]`

1. Run the `yarn run codegen:[subgraph]` command to prepare the TypeScript sources for the GraphQL (generated/schema) and the ABIs (generated/[ABI]/\*)
2. [Optional] run the `yarn run build:[subgraph]` command to build the subgraph. Can be used to check compile errors before deploying.
3. Run `graph auth https://api.thegraph.com/deploy/ <ACCESS_TOKEN>`
4. Deploy via `yarn run deploy:[subgraph]`.

## To query these subgraphs

Please use our node utility: [fera-data](https://github.com/feraswap/fera-data).

Note: This is in on going development as well.

## Example Queries

We will add to this as development progresses.

### Maker

```graphql
{
  maker(id: "0x6684977bbed67e101bb80fc07fccfba655c0a64f") {
    id
    servings(orderBy: timestamp) {
      id
      server {
        id
      }
      tx
      pair
      token0
      token1
      feraServed
      block
      timestamp
    }
  }
  servers {
    id
    feraServed
    servings(orderBy: timestamp) {
      id
      server {
        id
      }
      tx
      pair
      token0
      token1
      fera
      block
      timestamp
    }
  }
}
```

# Community Subgraphs

1) croco-finance fork of this repo with slight modifications - [deployment](https://thegraph.com/explorer/subgraph/benesjan/fera-swap), [code](https://github.com/croco-finance/feraswap-subgraph)
2) croco-finance dex-rewards-subgraph which tracks SLPs in MasterChef and all the corresponding rewards individually. (can be used for analysis of user's positions) - [deployment](https://thegraph.com/explorer/subgraph/benesjan/dex-rewards-subgraph), [code](https://github.com/croco-finance/dex-rewards-subgraph)
