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
    consider this code:
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