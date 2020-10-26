# Refactoring

# Grid representing the data of board 

From Narawish's Game of life code: https://github.com/NarawishS/pa4-NarawishS/

## setState() Method
in the src/gameOfLife/Grid.java class
https://github.com/NarawishS/pa4-NarawishS/blob/master/src/gameOfLife/Grid.java

consider this code:
```
public void setState(int x, int y, int state) {
        if (x < this.width && y < this.height && x >= 0 && y >= 0)
            this.grid[x][y] = state;
    }
```
- Refactoring Signs:
    - It has a complex and long if expression.

- Refactoring: extract variable
    - Assign each part of the expression to the new variable.
    - Replace part of the expression with the new variable.
```
public void setState(int x, int y, int state) {
        final boolean isXInGrid = x < this.width;
        final boolean isYInGrid = y < this.height;
        final boolean isXPositive = x >= 0;
        final boolean isYPositive = y >= 0;

        if (isXInGrid && isYInGrid && isXPositive && isYPositive)
            this.grid[x][y] = state;
    }
```

## countNeighbors() Method

consider this code:
```
public int countNeighbors(int x, int y) {
        int sum = 0;
        for (int i = -1; i < 2; i++) {
            for (int j = -1; j < 2; j++) {
                int col = (x + i);
                int row = (y + j);
                if (col >= 0 && col < width && row >= 0 && row < height)
                    sum += this.grid[col][row];
            }
        }
        sum -= this.grid[x][y];
        return sum;
    }
```
- Refactoring Signs:
    - Has a temporary variable that’s assigned the result of the equation.
    - It also has a complex and long if expression.

- Refactoring: use inline temp
    - Replace the references to the variable with the equation itself.
```
public int countNeighbors(int x, int y) {
        int sum = 0;
        for (int i = -1; i < 2; i++) {
            for (int j = -1; j < 2; j++) {
                if ((x + i) >= 0 && (x + i) < width && (y + j) >= 0 && (y + j) < height)
                    sum += this.grid[(x + i)][(y + j)];
            }
        }
        sum -= this.grid[x][y];
        return sum;
    }
```
- Refactoring: extract variable
    - Assign each part of the expression to the new variable.
    - Replace part of the expression with the new variable.
```
public int countNeighbors(int x, int y) {
        int sum = 0;
        for (int i = -1; i < 2; i++) {
            for (int j = -1; j < 2; j++) {
                boolean isColPositive = (x + i) >= 0;
                boolean isColInRange = (x + i) < width;
                boolean isRowPositive = (y + j) >= 0;
                boolean isRowInRange = (y + j) < height;
                if (isColPositive && isColInRange && isRowPositive && isRowInRange)
                    sum += this.grid[(x + i)][(y + j)];
            }
        }
        sum -= this.grid[x][y];
        return sum;
    }
```