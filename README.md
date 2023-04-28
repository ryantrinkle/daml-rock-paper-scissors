# Rock Paper Scissors App
Daml templates designed for a platform for playing Rock Paper Scissors with betting.

### I. Overview
Rock Paper Scissors (RPS) is a schoolyard game in which two players 

### II. Workflow

1. A game is initiated by a party (Player 1) proposing a game to another.  Player 1 includes some money in their proposal, and names the other party (Player 2) with whom they wish to play.  To accept the proposal and start a game, Player 2 must provide a bet equal to Player 1's bet.

2. Once the game is started, it proceeds in two phases.  In Phase 1, each player commits to a move.  The move is stored as a separate contract on-chain, and is not revealed to the other player.  The players may commit in any order, but each player may only commit once.  Phase 1 ends when both players have committed to their moves.

3. In Phase 2, each player reveals their move from Phase 1.  This allows both players to see that the game was conducted fairly.  Players may reveal their moves in any order.  Phase 2 ends when both players have revealed their moves.

4. When Phase 2 ends, the game automatically ends and pays out the winnings appropriately.  If one player has won the game, then both players' bets are paid to that player.  If the game is a draw, each player's bet is returned to that player.

### III. Challenge(s)
* These templates only implement a toy concept of money.  Although the payout logic is correct, additional work would be required to properly escrow and disburse real assets.
* It is possible for either party to prevent the game from progressing at either Phase 1 or Phase 2, and thus keep both parties' assets locked in the Game contract.  This would function as a denial of service attack, which would initiate an out-of-band ultimatum game, most likely destroying the economics of this game.  A potential solution would be to apply a timeout to the game, such that, after a certain amount of time has passed, either player may exercise a choice that causes them to win if the other player has not made a move.  Note that these situations *must* be treated as a win, not a draw, otherwise an incentive to avoid revealing losing moves remains.

### IV. Building
To compile the project
```
$ daml build
```

### V. Testing
To test all scripts:
Either run the pre-written script in the `Test.daml` under /daml OR run:
```
$ daml start
```

### VI. Running
To load the project into the sandbox and start navigator:
```
$ daml start
```
