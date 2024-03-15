N = 8  # Número de reinas y tamaño del tablero

# Función para imprimir el tablero
def print_board(board):
    for row in board:
        print(" ".join(row))
    print("\n")

# Función para verificar si una posición es segura para colocar una reina
def is_safe(board, row, col):
    # Verificar la fila hacia la izquierda
    for i in range(col):
        if board[row][i] == 'Q':
            return False
    
    # Verificar la diagonal superior hacia la izquierda
    for i, j in zip(range(row, -1, -1), range(col, -1, -1)):
        if board[i][j] == 'Q':
            return False
    
    # Verificar la diagonal inferior hacia la izquierda
    for i, j in zip(range(row, N, 1), range(col, -1, -1)):
        if board[i][j] == 'Q':
            return False
    
    return True

# Función para resolver el problema de las 8 reinas utilizando backtracking
def solve_queens(board, col):
    if col >= N:  # Todas las reinas han sido colocadas correctamente
        print_board(board)
        return True
    
    # Probar todas las filas en esta columna
    for i in range(N):
        if is_safe(board, i, col):
            # Colocar la reina en esta posición
            board[i][col] = 'Q'

            # Llamar recursivamente para colocar las reinas restantes
            if solve_queens(board, col + 1):
                return True
            
            # Si no se puede colocar una reina en esta posición, retroceder
            board[i][col] = '.'

    # Si no se puede colocar ninguna reina en esta columna
    return False

def main():
    # Inicializar el tablero con todas las casillas vacías
    board = [['.' for _ in range(N)] for _ in range(N)]
    
    # Llamar a la función para resolver el problema de las 8 reinas
    if not solve_queens(board, 0):
        print("No se encontró solución")

if __name__ == "__main__":
    main()
