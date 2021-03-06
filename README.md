# Pine Finance

> Protocol for decentralized & automated orders.

**TL;DR**: [Traders](#traders) can create orders. [Relayers](#relayers) can earn a fee executing them when the trade conditions can be fulfilled.

## Table of Contents

- [Introduction](#introduction)
- [Contracts](#contracts)
- [Interaction & Order Fulfillment](#interaction-and-order-fulfillment-example)

## Contracts

### Mainnet

- [PineCore](https://etherscan.io/address/0xd412054cca18a61278ced6f674a526a6940ebd84#code)

- [LimitOrdersModule](https://etherscan.io/address/0x037fc8e71445910e1e0bbb2a0896d5e9a7485318#code)

- [UniswapV1Handler](https://etherscan.io/address/0xf48f47c959951b1a8b0691159a75a035dfed2d1d#code)

- [UniswapV2Handler](https://etherscan.io/address/0x842a8dea50478814e2bfaff9e5a27dc0d1fdd37c#code)

### Rinkeby

- [PineCore](https://rinkeby.etherscan.io/address/0xd412054cca18a61278ced6f674a526a6940ebd84#code)

- [LimitOrdersModule](https://rinkeby.etherscan.io/address/0x037fc8e71445910e1e0bbb2a0896d5e9a7485318#code)

- [UniswapV1Handler](https://rinkeby.etherscan.io/address/0x9d8453c495ac68cf717179d5ad9235f5eebf387d#code)

- [UniswapV2Handler](https://rinkeby.etherscan.io/address/0xbf95dd8dfbccdba150b4bc3d227a80c53acd3e0f#code)

## Introduction

[Pine Finance](https://pine.finance) is a protocol for automated and decentralized orders exchange powered by Ethereum.

[Limit orders](https://www.investopedia.com/terms/l/limitorder.asp) give traders complete control over the rate at which their orders will be executed, enabling traders to automate transactions at a specific rate.

It continues the base commitment to free and decentralized exchange.

Every token combination is available. There **isn't** a limitation on how you can select what to buy and what to sell (Of course if it is a token living on the Ethereum network).

An order at Pine Finance can only be canceled by its creator, and it can be executed if the creator receives the desired amount, making the system trustless and independent of a central entity.

The [smart contract](https://etherscan.io/address/0xd412054cca18a61278ced6f674a526a6940ebd84#code) is validated and can be reviewed by anyone. The code hasn't been audited by a reputable third party yet, and we advise to proceed with caution.

[More info of how it works](https://medium.com/@pine_eth/pine-finance-an-amm-orders-engine-525fe1f1b1eb)

## Interaction and order fulfillment example

Imagine the current rate of DAI -> ETH is `0.003`. So, based on the market price if the _user_ trades `400 DAI` will receive `1.2 ETH`. **BUT**, a _user_ wants to sell `400 DAI` in exchange for `1.6 ETH` (`desired_output`).

The _user_ creates a limit order at [pine.finance](https://pine.finance) by sending a transaction with the following values:

- **Input**: 400 DAI
- **Rate**: 0.004 DAI-ETH
- **Output**: 1.6 ETH

Once the transaction is confirmed, _relayers_ will start checking if the order can be fulfilled. _Reyalers_ can have their own strategy on how to execute an order. Pine, has a minimum of two relayers running 24/7 with a basic strategy.

The first thing they do is to check how much _output_, in this case ETH, they will get in exchange for `400 DAI` (`trade_output`). Then, if it is higher or equal than `1.6 ETH` (which is what the _user_ set as the minimum output) they check how much will cost to send the transaction to do the trade (`execution cost`). Once _relayers_ get the `execution_cost`, they check if they can still achieve the output defined by the _user_:

```
desired_output <= (trade_output - execution_cost)
```

`execution_cost` depends on the [Gas Price](https://etherscan.io/gastracker). Higher gas prices, higher `execution_cost`. You can read more about Gas Price [here.](https://www.investopedia.com/terms/g/gas-ethereum.asp#:~:text=On%20the%20ethereum%20blockchain%2C%20gas,with%20are%20worth%200.000000001%20ether)

Finally, _relayers_ can charge a fee for executing the order (`relayer_fee`). The final formula will be:

```
desired_output <= (trade_output - execution_cost - relayer_fee)
```

_Even the math can match, have in mind that if the amount to trade is high, a price impact will occur depending on the liquidity of the pool used._

To continue with real numbers, if the `execution_cost` is 0.04 ETH and the `relayers_fee` is 0.006:

```
1.6 ETH <= trade_output - 0.04 ETH - 0.006 ETH

1.6 ETH <= trade_output - 0.046 ETH

1.6 ETH + 0.046 ETH <= trade_output

1.646 ETH <= trade_output // Final rate 0.004115 for execution
```

If you want to add your token reach out us.

- [Discord](https://discord.gg/w6JVcrg)
- [Telegram](https://t.me/UniswapEX)
- [Twitter](https://twitter.com/pine_eth)

Repo forked and modified from [Uniswap](https://github.com/Uniswap/uniswap-frontend).

Donate: [Gitcoin](https://gitcoin.co/grants/765/pine-finance-ex-uniswapex-v2)

