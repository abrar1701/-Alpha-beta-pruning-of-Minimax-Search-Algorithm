<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name: Mohamed Abrar M      </h3>
<h3>Register Number: 212223040111           </h3>
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
<hr>
<H3>Program:</H3>

```py
import math

HUMAN = 'X'
AI = 'O'
EMPTY = ' '

def print_board(board):
    print("-------------")
    for i in range(3):
        print(f"| {board[i*3]} | {board[i*3+1]} | {board[i*3+2]} |")
        print("-------------")

def check_winner(board):
    wins = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],
        [0, 3, 6], [1, 4, 7], [2, 5, 8],
        [0, 4, 8], [2, 4, 6]
    ]
    
    for w in wins:
        if board[w[0]] == board[w[1]] == board[w[2]] and board[w[0]] != EMPTY:
            return board[w[0]]
            
    if EMPTY not in board:
        return 'Tie'
        
    return None

def minimax(board, depth, is_maximizing, alpha, beta):
    result = check_winner(board)
    
    if result == AI:
        return 10 - depth
    elif result == HUMAN:
        return -10 + depth
    elif result == 'Tie':
        return 0

    if is_maximizing:
        max_eval = -math.inf
        for i in range(9):
            if board[i] == EMPTY:
                board[i] = AI
                eval = minimax(board, depth + 1, False, alpha, beta)
                board[i] = EMPTY
                
                max_eval = max(max_eval, eval)
                alpha = max(alpha, eval)
                
                if beta <= alpha:
                    break 
        return max_eval
    else:
        min_eval = math.inf
        for i in range(9):
            if board[i] == EMPTY:
                board[i] = HUMAN
                eval = minimax(board, depth + 1, True, alpha, beta)
                board[i] = EMPTY
                
                min_eval = min(min_eval, eval)
                beta = min(beta, eval)
                
                if beta <= alpha:
                    break
        return min_eval

def get_best_move(board):
    best_val = -math.inf
    best_move = -1
    alpha = -math.inf
    beta = math.inf

    for i in range(9):
        if board[i] == EMPTY:
            board[i] = AI
            move_val = minimax(board, 0, False, alpha, beta)
            board[i] = EMPTY
            
            if move_val > best_val:
                best_move = i
                best_val = move_val
                
    return best_move

def play_game():
    board = [EMPTY] * 9
    print("Tic-Tac-Toe: You are X, AI is O")
    print_board(board)

    while True:
        while True:
            try:
                move = int(input("Enter position (1-9): ")) - 1
                if 0 <= move <= 8 and board[move] == EMPTY:
                    board[move] = HUMAN
                    break
                else:
                    print("Invalid move, try again.")
            except ValueError:
                print("Please enter a number.")

        print_board(board)
        
        result = check_winner(board)
        if result:
            if result == HUMAN: print("You Win!")
            elif result == 'Tie': print("It's a Tie!")
            break

        print("AI is thinking...")
        ai_move = get_best_move(board)
        board[ai_move] = AI
        print_board(board)

        result = check_winner(board)
        if result:
            if result == AI: print("AI Wins!")
            elif result == 'Tie': print("It's a Tie!")
            break

if __name__ == "__main__":
    play_game()
```

<H3>Output:</H3>

```
Tic-Tac-Toe: You are X, AI is O
-------------
|   |   |   |
-------------
|   |   |   |
-------------
|   |   |   |
-------------
Enter position (1-9): 1
-------------
| X |   |   |
-------------
|   |   |   |
-------------
|   |   |   |
-------------
AI is thinking...
-------------
| X |   |   |
-------------
|   | O |   |
-------------
|   |   |   |
-------------
Enter position (1-9): 9
-------------
| X |   |   |
-------------
|   | O |   |
-------------
|   |   | X |
-------------
AI is thinking...
-------------
| X | O |   |
-------------
|   | O |   |
-------------
|   |   | X |
-------------
Enter position (1-9): 8
-------------
| X | O |   |
-------------
|   | O |   |
-------------
|   | X | X |
-------------
AI is thinking...
-------------
| X | O |   |
-------------
|   | O |   |
-------------
| O | X | X |
-------------
Enter position (1-9): 3
-------------
| X | O | X |
-------------
|   | O |   |
-------------
| O | X | X |
-------------
AI is thinking...
-------------
| X | O | X |
-------------
|   | O | O |
-------------
| O | X | X |
-------------
Enter position (1-9): 4
-------------
| X | O | X |
-------------
| X | O | O |
-------------
| O | X | X |
-------------
It's a Tie!
```
<H3>Result:</H3>
We have successfully implemented Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game


