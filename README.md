# Sudoku Solver

## Title Page
(Sudoku Solver Project)

## Introduction
This is a Python-based Sudoku Solver that allows users to either enter their own Sudoku puzzle or use a pre-defined sample puzzle for practice. The program then solves the puzzle using the **Backtracking Algorithm**.

## Methodology
1. The user is prompted to either enter their own Sudoku puzzle or use a default one.
2. The Sudoku board is processed using the **Backtracking Algorithm**.
3. The algorithm attempts to place numbers in empty cells while checking constraints.
4. If a valid solution is found, the solved board is displayed.
5. If no solution exists, the user is informed.

## Code Typed
```python
def is_valid(board, row, col, num):
    """Check if 'num' can be placed at board[row][col]."""
    
    # Check row and column
    for i in range(9):
        if board[row][i] == num or board[i][col] == num:
            return False
    
    # Check 3x3 grid
    box_x, box_y = (row // 3) * 3, (col // 3) * 3
    for i in range(3):
        for j in range(3):
            if board[box_x + i][box_y + j] == num:
                return False
    
    return True

def solve_sudoku(board):
    """Solve Sudoku using backtracking."""
    
    for row in range(9):
        for col in range(9):
            if board[row][col] == 0:  # Find empty cell
                for num in range(1, 10):  # Try numbers 1-9
                    if is_valid(board, row, col, num):
                        board[row][col] = num
                        if solve_sudoku(board):
                            return True
                        board[row][col] = 0  # Backtrack
                return False  # No valid number found
    
    return True

def print_board(board):
    """Print the Sudoku board."""
    for row in board:
        print(" ".join(map(str, row)))

# Welcome message
print("\nWelcome to Sudoku Solver!\n")

# User input or default Sudoku
choice = input("Enter your own Sudoku? (Yes/No): ").strip().lower()

if choice == 'yes':
    print("Enter 9 rows (use 0 for empty cells):")
    sudoku_board = [list(map(int, input().split())) for _ in range(9)]
else:
    sudoku_board = [
        [5, 3, 0, 0, 7, 0, 0, 0, 0],
        [6, 0, 0, 1, 9, 5, 0, 0, 0],
        [0, 9, 8, 0, 0, 0, 0, 6, 0],
        [8, 0, 0, 0, 6, 0, 0, 0, 3],
        [4, 0, 0, 8, 0, 3, 0, 0, 1],
        [7, 0, 0, 0, 2, 0, 0, 0, 6],
        [0, 6, 0, 0, 0, 0, 2, 8, 0],
        [0, 0, 0, 4, 1, 9, 0, 0, 5],
        [0, 0, 0, 0, 8, 0, 0, 7, 9]
    ]
    print("Using default Sudoku for practice.")

# Solve and print result
if solve_sudoku(sudoku_board):
    print("\nSolved Sudoku:")
    print_board(sudoku_board)
    print("\nThanks for using Sudoku Solver!\n")
else:
    print("No solution exists.")
```



