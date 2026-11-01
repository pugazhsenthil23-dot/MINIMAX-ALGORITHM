# Experiment 1(c): Implementation of MINIMAX Algorithm

## Aim

To implement the MINIMAX algorithm.

## Scenario: AI vs. Human Player – Winning Move Situation

The AI plays as Player X, and the human plays as Player O. It is the AI's turn, and the AI must identify the best winning move using the Minimax algorithm.

The game uses a 3×3 Tic-Tac-Toe board.

## Procedure / Algorithm

1. Define constants:

   * `PLAYER_X = 1`
   * `PLAYER_O = -1`
   * `EMPTY = 0`
2. Create `evaluate(board)` to check rows, columns, and diagonals for a winner.
3. Create `isMovesLeft(board)` to check whether empty cells are available.
4. Implement the recursive `minimax(board, isMax)` function.
5. If Player X wins, return 1. If Player O wins, return -1.
6. If no moves remain, return 0.
7. For Player X, choose the maximum score.
8. For Player O, choose the minimum score.
9. Implement `findBestMove(board)` to identify the best move for Player X.
10. Display the initial board, make the AI move, and display the updated board.

## Program

```python
PLAYER_X = 1
PLAYER_O = -1
EMPTY = 0

def evaluate(board):
    for row in range(3):
        if board[row][0] == board[row][1] == board[row][2] != EMPTY:
            return board[row][0]

    for col in range(3):
        if board[0][col] == board[1][col] == board[2][col] != EMPTY:
            return board[0][col]

    if board[0][0] == board[1][1] == board[2][2] != EMPTY:
        return board[0][0]

    if board[0][2] == board[1][1] == board[2][0] != EMPTY:
        return board[0][2]

    return 0

def isMovesLeft(board):
    for row in range(3):
        for col in range(3):
            if board[row][col] == EMPTY:
                return True
    return False

def minimax(board, isMax):
    score = evaluate(board)

    if score == PLAYER_X:
        return score

    if score == PLAYER_O:
        return score

    if not isMovesLeft(board):
        return 0

    if isMax:
        best = -float('inf')

        for row in range(3):
            for col in range(3):
                if board[row][col] == EMPTY:
                    board[row][col] = PLAYER_X
                    best = max(best, minimax(board, False))
                    board[row][col] = EMPTY

        return best

    else:
        best = float('inf')

        for row in range(3):
            for col in range(3):
                if board[row][col] == EMPTY:
                    board[row][col] = PLAYER_O
                    best = min(best, minimax(board, True))
                    board[row][col] = EMPTY

        return best

def findBestMove(board):
    bestVal = -float('inf')
    bestMove = (-1, -1)

    for row in range(3):
        for col in range(3):
            if board[row][col] == EMPTY:
                board[row][col] = PLAYER_X
                moveVal = minimax(board, False)
                board[row][col] = EMPTY

                if moveVal > bestVal:
                    bestMove = (row, col)
                    bestVal = moveVal

    return bestMove

def printBoard(board):
    for row in board:
        print(" ".join(
            ["X" if x == PLAYER_X else "O" if x == PLAYER_O else "." for x in row]
        ))

board = [
    [PLAYER_X, PLAYER_O, PLAYER_X],
    [PLAYER_O, PLAYER_X, EMPTY],
    [EMPTY, PLAYER_O, EMPTY]
]

print("Before AI Move:")
printBoard(board)

bestMove = findBestMove(board)

if bestMove != (-1, -1):
    board[bestMove[0]][bestMove[1]] = PLAYER_X

print("\nAfter AI Move:")
printBoard(board)
```

## Expected Output

```text
Before AI Move:
X O X
O X .
. O .

After AI Move:
X O X
O X X
. O .
```

## Result

Thus, the MINIMAX algorithm was implemented successfully, and the AI identified a winning move in the Tic-Tac-Toe game.

```

## Important correction
The manual's original starting board already contains a winning diagonal for X. I changed its bottom-right cell to empty so the AI can demonstrate the intended winning move. The algorithm and procedure follow the manual.

## Progress

| Experiment | Topic | Status |
|---|---|---|
| 1(a) | Eight Queens | Completed |
| 1(b) | Depth First Search | Completed |
| 1(c) | Minimax Algorithm | Current |
| 1(d) | A* Algorithm | Pending |
| 2(a) | Minimum and Maximum | Pending |
| 2(a) | Simple Clauses | Pending |
| 2(b) | Unification and Resolution | Pending |
| 2(c) | Backward Chaining | Pending |
| 2(d) | Forward Chaining | Pending |
| 3(a) | Blocks World | Pending |
| 3(b) | Fuzzy Inference System | Pending |

**Total: 3 of 11 presented.**

After creating this repository, type **NEXT** for Experiment 1(d) – A* Algorithm.
```
