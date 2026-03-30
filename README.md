# TARON MINER

CPU miner for the TARON blockchain — pool and solo mode. Standalone, no node required for pool mode.

## 0% Fees

## Which binary to use?

| Binary | CPUs |
|--------|------|
| `taron-miner-avx2` | AMD Ryzen (Zen 1/2/3), Intel Haswell and newer — **use this if unsure** |
| `taron-miner-avx512` | AMD Ryzen 7000+, Intel Ice Lake and newer |

If you get `Illegal instruction`, switch to `taron-miner-avx2`.

---

## Pool mode

Connect to a mining pool. No node required.

```bash
./taron-miner-avx2 --pool http://mypool.com:8083 --worker rig1 --threads 16
```

### Options

| Flag | Short | Default | Description |
|------|-------|---------|-------------|
| `--pool` | `-p` | — | Pool HTTP URL |
| `--address` | `-a` | — | Mining address (tar1...), overrides wallet file |
| `--worker` | `-n` | `default` | Worker name (identifies this rig) |
| `--threads` | `-t` | `0` (all physical cores) | Number of mining threads |
| `--wallet` | `-w` | `~/.taron-testnet/pool-miner.key` | Wallet key file |

---

## Solo mode

Mine directly on a TARON node. Requires a running node with RPC enabled.

### 1. Start the node with RPC

```bash
taron node start --rpc-port 8080
```

### 2. Expose RPC over the network (if miner is on a different machine)

The node RPC only listens on `127.0.0.1` by default. Use `socat` to expose it on the network:

```bash
# On the node machine
socat TCP-LISTEN:8081,fork,reuseaddr TCP:127.0.0.1:8080
```

### 3. Start the miner

```bash
./taron-miner-avx2 --node http://192.168.1.x:8081 --address tar1... --threads 16
```

If the miner runs on the same machine as the node:

```bash
./taron-miner-avx2 --node http://localhost:8080 --threads 16
```

### Options

| Flag | Short | Default | Description |
|------|-------|---------|-------------|
| `--node` | — | — | Node RPC URL |
| `--address` | `-a` | — | Mining address (tar1...), overrides wallet file |
| `--threads` | `-t` | `0` (all physical cores) | Number of mining threads |
| `--wallet` | `-w` | `~/.taron-testnet/pool-miner.key` | Wallet key file |

---

## Output

```
TARON MINER v0.1.0
  Address : tar1...
  Pool    : http://mypool.com:8083
  Worker  : rig1
  Threads : 16

[work] New block #147500 (share_diff=19)
[share] #147500 accepted nonce=3849201748
[stats] 13.2 kH/s | accepted=1 rejected=0 | blocks=0 | block=#147500
```

---

## Benchmarks

| CPU | Threads | Hashrate |
|-----|---------|----------|
| Ryzen 9 9950X | 30 | 13.2 kH/s |
| Ryzen 9 7950X | 30 | 12.9 kH/s |
| EPYC 7b12     | 120 | 35.1 kH/s |
