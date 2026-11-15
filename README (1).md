# 🐑 Sheep — dice game (Group A)

A browser version of **Sheep**, the two-dice push-your-luck game from our MATH group project, with the strategies from our report built in.

▶ **Play online:** https://smyez1.github.io/sheep-game/

<img src="qr.png" alt="QR code to the game" width="220">

Scan the QR code with a phone camera to open the game.

## Rules

Two players take turns. On each turn a player keeps throwing two dice until one of these happens, or they choose to **hold**:

| Throw | Result |
|---|---|
| Exactly one 6 | The turn scores nothing and ends |
| Double 6 | The turn scores nothing **and the player's total score resets to 0** |
| No 6 | The sum is **added** to the turn total, and the player may roll again or hold |
| Hold | The turn total is added to the player's total score |

The first player to reach **100 or more** wins.

## Features

- **vs Computer** or **2 Players** (two people pass one phone between them)
- A choice of four computer strategies (see below)
- An optional strategy panel showing, in every state, P(win) if you hold vs if you roll, the optimal move, what the practical and EV rules would do, and each player's win chance under optimal play

## Strategies

Notation: *i* = your score, *j* = opponent's score, *k* = turn total.

| Strategy | Decision rule | Win % vs optimal* |
|---|---|---|
| Optimal policy | maximise P(win) in every state via value iteration on V = max(H, R) | 50.0 |
| Practical rule | if j ≥ 80 roll until reaching 100; otherwise hold at k ≥ 15 + round((j − i)/8) | 48.9 |
| Hold at 15 | hold at k ≥ 15 | 47.2 |
| Expected-value rule | roll while 11k + i < 150 | 45.2 |

\*Exact policy evaluation against the optimal player, averaged over moving first and second. Every rule also holds as soon as banking would reach 100. With both players optimal, the first player wins 51.4%.

### How the optimal policy is stored

`V(i, j, 0)`, the probability that the player to move wins at the start of a turn, is precomputed for all 100 × 100 score pairs by Gauss–Seidel value iteration (tolerance 1e-12, 98 sweeps) and embedded in `index.html`. During a turn, the page rebuilds V(i, j, k) exactly by backward recursion over k:

- H(i, j, k) = 1 − V(j, i + k, 0)
- R(i, j, k) = 10/36 · (1 − V(j, i, 0)) + 1/36 · (1 − V(j, 0, 0)) + Σ_s ways(s)/36 · V(i, j, k + s)
- V(i, j, k) = max(H, R), and V = 1 once i + k ≥ 100
