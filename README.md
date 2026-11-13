# clone-lin-maker-clipper-kick

Experimental **LIN** clone of MakerDAO / Sky `Clipper.kick` — the Dutch-auction
start (`top = rmul(getFeedPrice(), buf)` and keeper `coin = add(tip, wmul(tab, chip))`).

**Proofs live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open)** — this repo is the LIN copy only.

- **Upstream (hash-pinned, not vendored):** [makerdao/dss](https://github.com/makerdao/dss) `fa4f6630afb0624d04a003e920b0d71a00331d98`
  - `src/clip.sol` sha256 `1ea897fc0e8e0964a2e5098716d86fdcd93d11e0b2e4f65998eb1b7650d167de` blob `c43d8fff46a4ad225d1fa031b4b1de618345cba7`
  - License AGPL-3.0-or-later. This repository does **not** vendor the Solidity source.
- **LIN kernel:** [`src/lin_maker_clipper_kick.lin`](src/lin_maker_clipper_kick.lin) (identical to lin-open)
- **C11 oracle copy:** [`test/oracles/maker_clipper_kick_c11.c`](test/oracles/maker_clipper_kick_c11.c)
- **Transpilable kernel:** [`test/oracles/maker_clipper_kick_kernel.c`](test/oracles/maker_clipper_kick_kernel.c)
- **Proofs (lin-open only):** `examples/maker_clipper_kick/` and `make maker-clipper-kick-proof`
- **Class:** EXPERIMENTAL uint64-scale. Not mainnet uint256 rad/wad/ray. Not a production clipper replacement.

Named goldens (`WAD=1000`, `RAY=1e6`, `BLN=1000`):

| id | call | value |
|---|---|---|
| FULL top | rmul(rdiv(mul(2000,BLN),1e6),1.1e6) | **2200000** |
| FULL coin | add(100, wmul(50000, 10)) | **600** |
| FULL id | kicks 7 + 1 | **8** |
| CHIP_ONLY | tip=0 chip=10 | **500** |
| TIP_ONLY | tip=100 chip=0 | **100** |
| PAR2 top | par=2e6 | **1100000** |

`stopped >= 1` and `auth != 1` fail-close. `7e9*3e9` tab*chip fail-closes while naive i64 wraps.
`val/par/buf/tip/chip` are arguments (Solidity uses OSM peek, storage chip/tip, `vat.suck`).

## Reproduce proofs (in lin-open)

```
make maker-clipper-kick-proof
```

## Not claimed

Uint256 rad/wad/ray / mainnet Clipper.kick / OSM / `vat.suck` host parity.
LIN replacing Maker, Sky, clipper, or the EVM. TVL or dollar savings. zk soundness.
`clipper.take` buy math. `dog.bark` lot sizing. Hidden `sales[]` maps.
