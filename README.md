# Building Uniswap Subgraph

**The Uniswap Protocol**  is a peer-to-peer system designed for exchanging cryptocurrencies on Ethereum blockchain.**Uniswap** acts like a autmated market maker where anyone can become **a liquidity provider** for a pool.

## Basic Functions of Uniswap

1. Anyone can add liquidity to become a liquidity provider.
2. Liquidity provider can remove their liquidity anytime and get back their crypto whenever they want.
3. Users can swap between assests present in the trading pool,assuming there is enough liquidity.
4. Users are charged small trading fees that gets distributed amongs the liquidity provider to provide an incetive for being a liquidity provider.


As of now, three versions of **uniswap** have been launched.The **first version** was launched on November, 2018 and it allowed swaps between ether and any other ERC20 token.

**V2** was launched in March 2020 and it was a huge improvement of V1 that allowed direct swaps between any ERC20 tokens, as well as chained swaps between any pairs.

**V3** was launched in May 2021 and it significantly improved capital efficiency, which allowed liquidity providers to remove a bigger portion of their liquidity from pools and still keep getting the same rewards.

## Smart Contract Overview

**Uniswap Smart Contract**  is a set of smart contracts which can be divided into **core** and **periphery**.

**Core contracts** provide fundamental safety guarantees for all parties interacting with Uniswap. They define the logic of pool generation, the pools themselves, and the interactions involving the respective assets therein.

**Periphery contracts** interact with one or more Core contracts but are not part of the core. They are designed to provide methods of interacting with the core that increase clarity and user safety.


## Core Contract Overview

The core contract has two main contract **UniswapV3Factory** and **UniswapV3Pool**.

The **factory contract** defines the logic for generating pools. A pool is defined by two tokens, which make up the asset pair, and a fee. There can be multiple pools of the same asset pair, distinguished only by their swap fee.The **UniswapV3Factory** have following functions:

* **createPool**
* **setOwner**
* **enableFeeAmount** 

This contract holds the following **state**:
* address public override owner
* mapping(uint24 => int24) public override feeAmountTickSpacing
* mapping(address => mapping(address => mapping(uint24 => address))) public override getPool;

The **UniswapV3Pool** is primarily serve as automated market makers for the paired assets.This contract has following functions:

* **_blockTimestamp**
* **snapshotCumulativesInside**
* **observe**
* **increaseObservationCardinalityNext**
* **initialize**
* **mint**
* **collect**
* **burn**
* **swap**
* **flash**
* **setFeeProtocol**
* **collectProtocol**

This contracts keep tracks of following **state**:

* address public immutable override factory;
* address public immutable override token0;
* address public immutable override token1;
* uint24 public immutable override fee;
* int24 public immutable override tickSpacing;
* uint128 public immutable override maxLiquidityPerTick;

