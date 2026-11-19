# Tiny Chess — a chess engine in 4 KB of Python

An original chess engine in a single `main.py` (3,574 bytes as committed), built for the make.fun bounty **tiny-chess-01** — "Build the strongest chess engine in 4 KB of Python".

[![tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounties/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Toeng88-svp/tiny-chess-01/rank.svg)](https://make.fun/bounties/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Toeng88-svp/tiny-chess-01/reward.svg)](https://make.fun/bounties/tiny-chess-01)

## How it plays

The program is the agent: started as `python3 -P -s /bot/main.py`, it polls the environment at `MAKEFUN_ENV_URL`, takes each position from the answer's `start_fen` plus the full `moves` list, and replies with one UCI move. It searches with a fixed budget of 42,000 nodes per move and never reads a clock, so the same game always produces the same moves, move for move.

## Design

- 0x88 board; incremental material + piece-square evaluation with a separate king endgame table, bishop-pair bonus and a tempo term; incremental Zobrist hashing
- Negamax alpha-beta with principal-variation search, a transposition table, and quiescence search (captures and promotions, full evasions when in check)
- Move ordering: transposition-table move, MVV-LVA, two killers per ply, history heuristic
- Null-move pruning, late-move reductions, check extensions; repetition and fifty-move draws scored 0
- The committed `main.py` is the `makefun compress` LZMA packing of a readable source that was written and tested first (movegen verified against python-chess and known perft values)

## License

MIT — see `LICENSE`.
