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
| No 6 | The sum goes into the turn total, and the player may roll again or hold |
| Hold | The turn total is added to the player's score |

The first player to reach **100 or more** wins.

## Modes

- **vs Computer**: play against a computer opponent
- **2 Players**: two people pass one phone between them
- An optional strategy hint, a Chinese / English interface, and it works on phones

## Strategy used by the hint and the computer

With turn total *t* and banked score *S*, one more throw of two dice changes the expected outcome by

E[gain] = (25/36)·6 − (10/36)·t − (1/36)·(t + S) = (150 − 11t − S)/36

so the player should roll while 11t + S < 150 (for example, hold at t ≥ 14 when S = 0), and always hold if holding reaches 100.
This rule maximises the expected score per turn. It is a good heuristic, but not the exact win-probability-optimal policy.
