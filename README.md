import random

def generate_mine_positions(n):
    num_mines = random.randint(1, n*n//3)
    mine_positions = [[0 for _ in range(n)] for _ in range(n)]
    for _ in range(num_mines):
        i, j = random.randint(0, n - 1), random.randint(0, n - 1)
        while mine_positions[i][j] == 1:
            i, j = random.randint(0, n - 1), random.randint(0, n - 1)
        mine_positions[i][j] = 1
    return mine_positions

def print_minesweeper(n, mine_positions):
    board = [[0 for _ in range(n)] for _ in range(n)]
    for i in range(n):
        for j in range(n):
            if mine_positions[i][j] == 1:
                board[i][j] = '*'
    for i in range(n):
        for j in range(n):
            if board[i][j] != '*':
                mine_count = 0
                for di in range(-1, 2):
                    for dj in range(-1, 2):
                        if 0 <= i + di < n and 0 <= j + dj < n and board[i + di][j + dj] == '*':
                            mine_count += 1
                board[i][j] = mine_count
    for row in board:
        print(' '.join(str(cell) for cell in row))
N = int(input("Enter the size of the grid (N): "))
mines = generate_mine_positions(N)
print_minesweeper(N, mines)
