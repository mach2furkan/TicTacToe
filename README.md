    #include <iostream>
            const char PLAYER1 = 'X';
    const char PLAYER2 = 'O';
            const int SIZE = 3;

                            // Function to initialize the board
      void initializeBoard(char board[][SIZE]) {
    for (int i = 0; i < SIZE; i++)
        for (int j = 0; j < SIZE; j++)
            board[i][j] = ' ';
        }

                            // Function to print the board
    void printBoard(char board[][SIZE]) {
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            std::cout << board[i][j];
            if (j < SIZE - 1) std::cout << " | ";
        }
        std::cout << std::endl;
        if (i < SIZE - 1) std::cout << "---------" << std::endl;
    }
      }
  
                // Function to check if someone has won
    bool checkWin(char board[][SIZE], char player) {
    // Check rows, columns, and diagonals
    for (int i = 0; i < SIZE; i++) {
        if (board[i][0] == player && board[i][1] == player && board[i][2] == player)
            return true;
    }
    for (int i = 0; i < SIZE; i++) {
        if (board[0][i] == player && board[1][i] == player && board[2][i] == player)
            return true;
    }
    if (board[0][0] == player && board[1][1] == player && board[2][2] == player)
        return true;
    if (board[0][2] == player && board[1][1] == player && board[2][0] == player)
        return true;
    return false;
      }

      // Function to check if the board is full
    bool isBoardFull(char board[][SIZE]) {
    for (int i = 0; i < SIZE; i++)
        for (int j = 0; j < SIZE; j++)
            if (board[i][j] == ' ')
                return false;
    return true;
    }

    // Main game function
    int main() {
    char board[SIZE][SIZE];
    int row, col;
    char currentPlayer = PLAYER1;
    initializeBoard(board);

    while (true) {
        printBoard(board);
        std::cout << "Player " << currentPlayer << ", enter row (0, 1, 2) and column (0, 1, 2): ";
        std::cin >> row >> col;

        // Input validation
        if (row >= 0 && row < SIZE && col >= 0 && col < SIZE && board[row][col] == ' ') {
            board[row][col] = currentPlayer;
        } else {
            std::cout << "Invalid move, try again." << std::endl;
            continue;
        }

        // Check for win or draw
        if (checkWin(board, currentPlayer)) {
            printBoard(board);
            std::cout << "Player " << currentPlayer << " wins!" << std::endl;
            break;
        } else if (isBoardFull(board)) {
            printBoard(board);
            std::cout << "It's a draw!" << std::endl;
            break;
        }

        // Switch player
        currentPlayer = (currentPlayer == PLAYER1) ? PLAYER2 : PLAYER1;
    }

    return 0;
}
