- 👋 Hi, I’m @Abhay4576
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
Abhay4576/Abhay4576 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import random

# Define candy types
CANDY_TYPES = ["R", "G", "B", "Y", "P"]  # R=Red, G=Green, B=Blue, Y=Yellow, P=Purple

# Define the board size
BOARD_SIZE = 5

# Initialize the game board
def create_board(size):
    return [[random.choice(CANDY_TYPES) for _ in range(size)] for _ in range(size)]

# Print the game board
def print_board(board):
    for row in board:
        print(" ".join(row))
    print("\n")

# Swap two candies on the board
def swap(board, x1, y1, x2, y2):
    board[x1][y1], board[x2][y2] = board[x2][y2], board[x1][y1]

# Find matches of three or more
def find_matches(board):
    matches = []
    # Check rows for matches
    for i in range(BOARD_SIZE):
        for j in range(BOARD_SIZE - 2):
            if board[i][j] == board[i][j+1] == board[i][j+2]:
                matches.append((i, j))
                matches.append((i, j+1))
                matches.append((i, j+2))

    # Check columns for matches
    for j in range(BOARD_SIZE):
        for i in range(BOARD_SIZE - 2):
            if board[i][j] == board[i+1][j] == board[i+2][j]:
                matches.append((i, j))
                matches.append((i+1, j))
                matches.append((i+2, j))
                
    return list(set(matches))  # Remove duplicates

# Clear matches and drop new candies
def clear_matches(board, matches):
    for i, j in matches:
        board[i][j] = None  # Clear the matched candies

    # Drop candies
    for j in range(BOARD_SIZE):
        empty_spots = [i for i in range(BOARD_SIZE) if board[i][j] is None]
        if empty_spots:
            for i in reversed(empty_spots):
                board[i][j] = random.choice(CANDY_TYPES)  # Add new random candy

# Run a simple game loop
def play_game():
    board = create_board(BOARD_SIZE)
    print("Initial Board:")
    print_board(board)
    
    while True:
        matches = find_matches(board)
        if matches:
            print("Matches found!")
            clear_matches(board, matches)
            print_board(board)
        else:
            print("No more matches. Exiting game.")
            break

play_game()
