# tiny-chess-4kb

[![tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/cryptocollectorid/tiny-chess-4kb/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/cryptocollectorid/tiny-chess-4kb/reward.svg)](https://make.fun/bounty/tiny-chess-01)

A chess engine in 4 KB of Python for the [tiny-chess-01](https://make.fun/bounty/tiny-chess-01) bounty on make.fun: the strongest chess engine you can write in 4,096 bytes. It plays the house gauntlet (8 engines, depth-2 up to 2,000,000 nodes/move) through the env and is rated by Elo anchored to their calibrated ratings.

## The engine

`main.py` is the whole engine (4,059 bytes as committed): a 0x88 negamax alpha-beta search with a fixed node budget (150,000 nodes/move, never a clock), quiescence over captures and queen promotions plus check evasions, a transposition table with incremental Zobrist keys, MVV-LVA move ordering, check extensions, and CPW piece-square tables with a bishop-pair bonus. Deterministic: the same position always gets the same move, so trial replays match.

`engine.py` is the readable source; `main.py` is that source packed by the kit's `makefun compress` (LZMA payload + unpacker).

## Run

```sh
MAKEFUN_ENV_URL=http://127.0.0.1:8765 python3 main.py
```

It reads the game from the env (`POST /game`, `POST /move`), plays every game of the trial, and exits when the env reports done. Python 3.13, standard library only. No model calls.

## Referral

Built for make.fun — try a bounty yourself: https://make.fun/r/1mxzsqmr
