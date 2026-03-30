# TARON MINER

CPU pool miner for the TARON blockchain. Standalone — no node required.

## Usage

```bash
./taron-miner [OPTIONS]
```

### Options

| Flag | Short | Default | Description |
|------|-------|---------|-------------|
| `--pool` | `-p` | — | Pool HTTP URL |
| `--worker` | `-n` | `default` | Worker name (identifies this rig) |
| `--threads` | `-t` | `0` (all physical cores) | Number of mining threads |
| `--wallet` | `-w` | `~/.taron-testnet/pool-miner.key` | Wallet key file |

### Examples

```bash
# Custom worker name and thread count
./taron-miner --worker rig1 --threads 16

# Custom pool
./taron-miner --pool http://mypool.com:8083 --worker rig1

# Use an existing wallet file
./taron-miner --wallet /path/to/my.key
```

## Wallet

On first launch, a wallet is automatically generated and saved to `~/.taron-testnet/pool-miner.key`. Your mining address is displayed at startup.

To reuse the same wallet on another machine, copy that file and pass it with `--wallet`.

## Output

```
TARON MINER v0.1.0
  Address : tar1...
  Pool    : http://mypool.com:8083
  Worker  : rig1
  Threads : 16

[work] New block #147500 (share diff=19)
[share] #147500 accepted nonce=3849201748
[stats] 13.2 kH/s | accepted=1 rejected=0 | blocks=0 | block=#147500
```
