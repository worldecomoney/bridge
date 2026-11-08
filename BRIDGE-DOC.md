# SmartNet Bridge

## Overview

SmartNet Bridge enables the transfer of native coins and ERC-20 tokens between SmartNet and supported external blockchain networks.

The bridge connects SmartNet to a predefined set of external networks and assets, allowing users to move funds in either direction while maintaining consistent asset accounting.

Unlike conventional liquidity-based bridges, SmartNet Bridge does not rely on large prefunded SmartNet balances. Incoming assets are represented on SmartNet through validator-authorized minting, while outgoing transfers are backed by the corresponding destruction of SmartNet funds.

## Supported Networks and Assets

SmartNet Bridge operates with a closed list of supported external networks and assets.

Each supported network has a registered external bridge address. Supported native coins and ERC-20 tokens have explicit mappings to their corresponding SmartNet assets.

Only configured networks, addresses, and tokens can participate in bridge operations.

## Fundamental Principles

SmartNet circulating funds can originate only from:

1. Preminted allocations established at genesis.
2. Verified deposits originating from supported external networks.

There is no independent or arbitrary source of monetary issuance.

Every bridged asset has a defined relationship between its external representation and its SmartNet representation.

The default conversion is 1:1 in economic units, accounting for differences in token decimals where applicable.

## Inbound Transfers

Inbound transfers move funds from an external network to SmartNet.

When a user sends native coins or supported ERC-20 tokens to a registered external bridge address, the bridge identifies and verifies the deposit.

Once the external transaction satisfies the required verification and confirmation conditions, the bridge submits a corresponding transaction to SmartNet through its normal transaction pool.

The SmartNet validator recognizes the registered bridge context and independently verifies the deposit before authorizing the corresponding mint operation.

The resulting funds become available on SmartNet through normal transaction execution.

## Outbound Transfers

Outbound transfers move funds from SmartNet to an external network.

A user initiates an outbound transfer by sending a normal SmartNet transaction to a registered bridge address.

The SmartNet validator recognizes the destination as a bridge address, validates the transaction, and burns the corresponding SmartNet funds as part of normal transaction execution.

After the withdrawal transaction is finalized, the bridge processes the corresponding external transfer.

The destination receives the equivalent native coin or ERC-20 token on the selected external network.

## Transaction Model

SmartNet Bridge uses the existing SmartNet transaction model.

Bridge operations do not require dedicated transaction types or a separate transaction execution mechanism.

Registered bridge addresses identify bridge-related transactions and determine their context.

Inbound transactions enter through the normal txpool, just like transactions submitted by wallets. Outbound transfers originate from ordinary user transactions to registered bridge addresses.

The validator remains the authority for all SmartNet balance changes, including minting and burning.

## Validation and Security

Bridge operations involve two independent blockchain environments.

The bridge performs external transaction discovery and preliminary verification, while the SmartNet validator independently determines whether an inbound operation is valid for execution.

External deposits must satisfy transaction success, asset identification, destination, amount, confirmation, and uniqueness requirements.

Outbound transfers are processed only after the corresponding SmartNet burn has been finalized.

Each external deposit and SmartNet withdrawal is uniquely identifiable, preventing the same operation from being processed more than once.

External transaction finality and blockchain reorganizations are taken into account when determining whether a deposit or withdrawal can be completed.

## Asset Accounting

SmartNet maintains a clear accounting relationship between incoming and outgoing bridge operations.

For each asset:

**Circulating Supply = Genesis Allocations + Bridge-In Minting − Bridge-Out Burning**
`Circulating Supply = Genesis Allocations + Bridge-In Minting - Bridge-Out Burning`
This establishes an auditable origin for SmartNet circulating funds and prevents the bridge from introducing unaccounted supply.

External reserves remain necessary to support outbound transfers.

## Operational Independence

The bridge operates as part of the SmartNet node lifecycle, alongside the validator and mesh.

It handles external network communication and bridge transaction processing without introducing an independent execution or consensus mechanism.

All changes to SmartNet state remain subject to the existing validator and transaction lifecycle.

## Summary

SmartNet Bridge provides a direct connection between SmartNet and supported external blockchain networks.

Its defining characteristics are:

- Closed network and asset support.
- Native coin and ERC-20 compatibility.
- No requirement for prefunded SmartNet liquidity.
- Validator-authorized inbound minting.
- Validator-executed outbound burning.
- Normal SmartNet transactions and txpool integration.
- Independent verification of external transactions.
- Transparent and auditable monetary accounting.

The result is a native bridge integrated into SmartNet's existing architecture rather than a separate liquidity-based transaction system.
