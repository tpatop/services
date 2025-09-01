# IBC Relayer Setup: Vota ↔ Osmosis

This document describes the IBC relayer deployed and maintained by our team for the **Vota mainnet**.

## Overview

- **Source chain:** Vota (`vota-ash`)
- **Destination chain:** Osmosis (`osmosis-1`)
- **Relayer software:** [Cosmos Relayer](https://github.com/cosmos/relayer)
- **Relayer path name:** `doravota-osmo`
- **Status:** ✅ Operational, running 24/7 with monitoring & autorestart

## Channel Details

| Chain       | Channel ID   | Port      | Connection ID  | State       |
|-------------|-------------|-----------|----------------|-------------|
| Vota        | `channel-17` | transfer  | `connection-41` | `STATE_OPEN` |
| Osmosis     | `channel-106136` | transfer  | `connection-10836` | `STATE_OPEN` |

- **Ordering:** `ORDER_UNORDERED`  
- **Version:** `ics20-1`

## Usage

The relayer is **permissionless** – any user can transfer tokens through the established channel.

Example transfer (from Vota → Osmosis):

```bash
votad tx ibc-transfer transfer transfer channel-17 \
  osmo1xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx \
  1000000peaka \
  --from <your_key> \
  --chain-id vota-ash \
  --fees 10000000000peaka
