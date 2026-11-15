# 🐑 Sheep — dice game

A browser version of **Sheep**, the two-dice push-your-luck game from our MATH group project (Project 1).

▶ **Play online:** https://smyez1.github.io/sheep-game/

<img src="qr.png" alt="QR code to the game" width="220">

Scan the QR code with a phone camera to open the game.

## Rules

Two players take turns. On each turn a player keeps throwing two dice until one of these happens, or they choose to **hold**:

| Throw | Result |
|---|---|
| Exactly one 6 | The turn scores nothing and ends |
| Double 6 | The turn scores nothing **and the player's total score resets to 0** |
| No 6 | The sum of this throw becomes the turn score (it **replaces** the previous throw, so at most 10), and the player may roll again or hold |
| Hold | The turn score is added to the player's total score |

The first player to reach **100 or more** wins.

## Modes

- **vs Computer**: play against a computer opponent
- **2 Players**: two people pass one phone between them
- An optional strategy hint, and it works on phones

## Strategy used by the hint and the computer

Let *v* be the current turn score (the latest throw) and *S* the banked score.
Holding banks *v*. Rerolling gives a new value *w* with probability 25/36 (sum of two dice showing 1–5), 0 with probability 10/36, and 0 plus the loss of *S* with probability 1/36 (double 6).
The expected gain *C* from rerolling and then playing on optimally satisfies

C = Σ_w P(w) · max(w, C) − S/36

and the player should **hold iff v ≥ C**, unless holding already reaches 100, in which case always hold.

| Banked score S | C | Hold when the throw is at least |
|---|---|---|
| 0 | 4.33 | 5 |
| 20 | 3.70 | 4 |
| 50 | 2.80 | 3 |
| 80 | 1.94 | 2 (always hold) |

This rule maximises the expected score per turn. It is a good heuristic, but not the exact win-probability-optimal policy.
