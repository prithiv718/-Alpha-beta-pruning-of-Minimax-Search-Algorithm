<h1>ExpNo 7 : Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game</h1> 
<h3>Name:  PRITHIV S     </h3>
<h3>Register Number/Staff Id:  212224020043         </h3>
<H3>Aim:</H3>
<p>
Implement Alpha-beta pruning of Minimax Search Algorithm for a Simple TIC-TAC-TOE game
</p>
<h1>GOALS of Alpha-Beta Pruning in MiniMax Search Algorithm</h1>
import math

# Tic-Tac-Toe game with Minimax and Alpha-Beta pruning
# Player is 'X', AI is 'O'

board = [' ' for _ in range(9)]


# Print Board
def print_board():
    print()
    for i in range(3):
        print(" | ".join(board[i*3:(i+1)*3]))
        if i < 2:
            print("--+---+--")
    print()


# Check Winner
def is_winner(b, player):

    win_conditions = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],   # Rows
        [0, 3, 6], [1, 4, 7], [2, 5, 8],   # Columns
        [0, 4, 8], [2, 4, 6]              # Diagonals
    ]

    for condition in win_conditions:
        if all(b[i] == player for i in condition):
            return True

    return False


# Check Board Full
def is_board_full(b):
    return ' ' not in b


# Evaluate Board
def evaluate(b):

    if is_winner(b, 'O'):
        return 1

    elif is_winner(b, 'X'):
        return -1

    else:
        return 0


# Minimax with Alpha-Beta Pruning
def minimax(b, depth, is_maximizing, alpha, beta):

    score = evaluate(b)

    if score == 1 or score == -1:
        return score

    if is_board_full(b):
        return 0

    # Maximizer (AI - O)
    if is_maximizing:

        max_eval = -math.inf

        for i in range(9):

            if b[i] == ' ':

                b[i] = 'O'
                eval = minimax(b, depth+1, False, alpha, beta)
                b[i] = ' '

                max_eval = max(max_eval, eval)
                alpha = max(alpha, eval)

                if beta <= alpha:
                    break   # Beta Cut-off

        return max_eval


    # Minimizer (Human - X)
    else:

        min_eval = math.inf

        for i in range(9):

            if b[i] == ' ':

                b[i] = 'X'
                eval = minimax(b, depth+1, True, alpha, beta)
                b[i] = ' '

                min_eval = min(min_eval, eval)
                beta = min(beta, eval)

                if beta <= alpha:
                    break   # Alpha Cut-off

        return min_eval


# Find Best Move
def best_move():

    best_val = -math.inf
    move = -1

    for i in range(9):

        if board[i] == ' ':

            board[i] = 'O'
            move_val = minimax(board, 0, False, -math.inf, math.inf)
            board[i] = ' '

            if move_val > best_val:
                best_val = move_val
                move = i

    return move


# Main Program
def main():

    print("Welcome to Tic-Tac-Toe!")
    print("You are X, AI is O")
    print_board()

    while True:

        # Player Move
        while True:
            try:
                user_move = int(input("Enter your move (1-9): ")) - 1

                if 0 <= user_move < 9 and board[user_move] == ' ':
                    board[user_move] = 'X'
                    break
                else:
                    print("Invalid move, try again.")

            except ValueError:
                print("Enter number between 1 to 9.")

        print_board()

        if is_winner(board, 'X'):
            print("You Win!")
            break

        if is_board_full(board):
            print("It's a Draw!")
            break


        # AI Move
        ai_move = best_move()
        board[ai_move] = 'O'

        print("AI placed O at position", ai_move + 1)
        print_board()

        if is_winner(board, 'O'):
            print("AI Wins!")
            break

        if is_board_full(board):
            print("It's a Draw!")
            break


# Run Program
if __name__ == "__main__":
    main()


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
<h2>Sample Input and Output:</h2>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/8d5e329a-9aff-41a6-bcf0-46efa10e1b92)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/438b242d-54ba-443e-b040-a936e6ae3b55)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/99a33390-fa11-4ade-a19f-e93bcd7aaec9)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/440797bd-53cb-49c1-b18d-89776864c3e7)
![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/81575a16-26b2-46f1-a8ac-27c9ed0a0fe5)
