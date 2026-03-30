# TARON MINER

CPU pool miner for the TARON blockchain. Standalone — no node required.

# 0% Fees

## Which binary to use?

| Binary | CPUs |
|--------|------|
| `taron-miner-avx2` | AMD Ryzen (Zen 1/2/3), Intel Haswell and newer — **use this if unsure** |
| `taron-miner-avx512` | AMD Ryzen 7000+, Intel Ice Lake and newer |

If you get `Illegal instruction`, switch to `taron-miner-avx2`.

## Usage

```bash
./taron-miner-avx2 [OPTIONS]
```

### Options

| Flag | Short | Default | Description |
|------|-------|---------|-------------|
| `--pool` | `-p` | — | Pool HTTP URL |
| `--address` | `-a` | — | Mining address (tar1...), overrides wallet file |
| `--worker` | `-n` | `default` | Worker name (identifies this rig) |
| `--threads` | `-t` | `0` (all physical cores) | Number of mining threads |
| `--wallet` | `-w` | `~/.taron-testnet/pool-miner.key` | Wallet key file |

### Examples

```bash
# Custom worker name and thread count
./taron-miner-avx2 --pool http://mypool.com:8083 --worker rig1 --threads 16

# Use an existing address
./taron-miner-avx2 --pool http://mypool.com:8083 --address tar1abc123...

# Use an existing wallet file
./taron-miner-avx2 --pool http://mypool.com:8083 --wallet /path/to/my.key
```

## Wallet

On first launch, a wallet is automatically generated and saved to `~/.taron-testnet/pool-miner.key`. Your mining address is displayed at startup.

To reuse the same wallet on another machine, copy that file and pass it with `--wallet`, or simply pass your address with `--address`.

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
