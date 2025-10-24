<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name: chaithanya chowla    </h3>
<h3>Register Number: 2305002004       </h3>
<H3>Aim:</H3>
<p>
Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game
</p>
<h1>GOALS of Alpha-Beta Pruning in MiniMax Search Algorithm</h1>

<h3>Improve the decision-making efficiency of the computer player by reducing the number of evaluated nodes in the game tree.</h3>
<h3>Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning and the Minimax algorithm with Python Code.</h3>
<h1>IMPLEMENTATION</h1>

The project involves developing a Tic-Tac-Toe game implementation incorporating the Alpha-Beta pruning with the Minimax algorithm. Using this algorithm, the computer player analyzes the game state, evaluates possible moves, and selects the optimal action based on the anticipated outcomes.

<h1>The Minimax algorithm</h1>

recursively evaluates all possible moves and their potential outcomes, creating a game tree.

<h1>Alpha-Beta pruning</h1>

Alpha–Beta (𝛼−𝛽) algorithm is actually an improved minimax using a heuristic. It stops evaluating a move when it makes sure that it’s worse than a previously examined move. Such moves need not to be evaluated further.

When added to a simple minimax algorithm, it gives the same output but cuts off certain branches that can’t possibly affect the final decision — dramatically improving the performance

## PROGRAM
```python
import time

class TicTacToe:
    def __init__(self):
        self.board = [['.' for _ in range(3)] for _ in range(3)]
        self.player = 'X'  # X always starts first

    def draw(self):
        for row in self.board:
            print(" | ".join(row))
        print()

    def valid_move(self, x, y):
        return 0 <= x < 3 and 0 <= y < 3 and self.board[x][y] == '.'

    def check_winner(self):
        # Check rows and columns
        for i in range(3):
            if self.board[i][0] == self.board[i][1] == self.board[i][2] != '.':
                return self.board[i][0]
            if self.board[0][i] == self.board[1][i] == self.board[2][i] != '.':
                return self.board[0][i]

        # Check diagonals
        if self.board[0][0] == self.board[1][1] == self.board[2][2] != '.':
            return self.board[0][0]
        if self.board[0][2] == self.board[1][1] == self.board[2][0] != '.':
            return self.board[0][2]

        # Check for draw
        if all(self.board[i][j] != '.' for i in range(3) for j in range(3)):
            return '.'

        return None  # Game not over

    # AI (O) tries to maximize score
    def max_value(self, alpha, beta):
        winner = self.check_winner()
        if winner == 'X': return -1, None, None
        if winner == 'O': return 1, None, None
        if winner == '.': return 0, None, None

        best = -2
        move = (None, None)

        for i in range(3):
            for j in range(3):
                if self.board[i][j] == '.':
                    self.board[i][j] = 'O'
                    val, _, _ = self.min_value(alpha, beta)
                    self.board[i][j] = '.'

                    if val > best:
                        best, move = val, (i, j)
                    alpha = max(alpha, best)
                    if beta <= alpha:
                        break
        return best, move[0], move[1]

    # Player (X) tries to minimize score
    def min_value(self, alpha, beta):
        winner = self.check_winner()
        if winner == 'X': return -1, None, None
        if winner == 'O': return 1, None, None
        if winner == '.': return 0, None, None

        best = 2
        move = (None, None)

        for i in range(3):
            for j in range(3):
                if self.board[i][j] == '.':
                    self.board[i][j] = 'X'
                    val, _, _ = self.max_value(alpha, beta)
                    self.board[i][j] = '.'

                    if val < best:
                        best, move = val, (i, j)
                    beta = min(beta, best)
                    if beta <= alpha:
                        break
        return best, move[0], move[1]

    def play(self):
        while True:
            self.draw()
            winner = self.check_winner()

            if winner:
                if winner == '.':
                    print("It's a tie!")
                else:
                    print(f"The winner is {winner}!")
                break

            if self.player == 'X':
                # Player's move
                try:
                    x, y = map(int, input("Enter row and column (0-2): ").split())
                    if self.valid_move(x, y):
                        self.board[x][y] = 'X'
                        self.player = 'O'
                    else:
                        print("Invalid move! Try again.")
                except:
                    print("Enter valid numbers like '1 2'")
            else:
                # AI's move
                start = time.time()
                _, x, y = self.max_value(-2, 2)
                end = time.time()
                print(f"AI took {round(end - start, 3)}s. Move: ({x}, {y})")
                self.board[x][y] = 'O'
                self.player = 'X'


if __name__ == "__main__":
    game = TicTacToe()
    game.play()

```
<hr>
<h2>Sample Input and Output:</h2>

<img width="812" height="737" alt="Screenshot 2025-10-22 094612" src="https://github.com/user-attachments/assets/f8dc462d-84e4-4e52-8a86-7e55c1358640" />
<img width="612" height="743" alt="Screenshot 2025-10-22 094756" src="https://github.com/user-attachments/assets/d422801a-2259-47b0-a86f-19dcd1e58b12" />


## RESULT
We have successfully implemented Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game.
