# Dora Vota — Snapshots (chain-id: `vota-ash`)

Up-to-date snapshots of the Dora Vota node for quick recovery of **full nodes** and **validators**.

---

## ⚡ Restore from Snapshot

### 0. Install required packages
Make sure the following tools are installed on your server:

```bash
sudo apt update
sudo apt install -y curl jq lz4 tar
```

---

### 1. Mandatory backup of validator files
Before doing anything, back up the file:

```bash
# current validator state (MANDATORY for validators)
cp $HOME/.dora/data/priv_validator_state.json ~/priv_validator_state.json.backup
```
> ❗ Without this file, a validator may trigger slashing for double-signing if restored incorrectly.


---

### 2. Stop the node

```bash
systemctl stop dorad
```

---

### 3. Remove old data

```bash
rm -rf $HOME/.dora/data $HOME/.dora/wasm
```

---

### 4. Download the latest snapshot and extract

```bash
H=$(curl -s http://snapshots.mooncore.pro/vota-ash/index.json | jq -r .height)

curl -L "http://snapshots.mooncore.pro/vota-ash/${H}.tar.lz4" \
  | lz4 -dc - | tar -xf - -C $HOME/.dora
```

---

### 5. Restore the file from backup

```bash
# restore validator state
cp ~/priv_validator_state.json.backup $HOME/.dora/data/priv_validator_state.json
```

---

### 6. Start the node
```bash
systemctl start dorad
```

---

### 7. Check logs
```bash
journalctl -u dorad -f
```

---

## 📂 Contents of the snapshot

data/ — blockchain database

wasm/ — CosmWasm codes and cache

data/priv_validator_state.json — an empty placeholder file (for full nodes).

> For validators it MUST be replaced with your own backed-up file.




---

## 🔗 Links

Metadata: http://snapshots.mooncore.pro/vota-ash/index.json

Archive: http://snapshots.mooncore.pro/vota-ash/HEIGHT.tar.lz4

Checksum: http://snapshots.mooncore.pro/vota-ash/HEIGHT.tar.lz4.sha256



---

✅ After restoration the node will continue syncing from the block height contained in the snapshot.

---
