# Valid Sudoku (Boolean Array Approach)

## Problem
You are given a `9 x 9` Sudoku board.

Each cell contains:
- a digit `'1'` to `'9'`, or
- a dot `'.'` meaning empty.

The task is to check whether the board is **valid** according to Sudoku rules:

- Each row must not contain duplicate digits `1–9`
- Each column must not contain duplicate digits `1–9`
- Each 3×3 sub-box must not contain duplicate digits `1–9`

Note: The Sudoku board does **not** need to be solved — only validated.

---

## Intuition
Sudoku validity is about **tracking duplicates**.

When we see a number, we must ensure:
- it has not appeared in the same **row**
- it has not appeared in the same **column**
- it has not appeared in the same **3×3 box**

To do this efficiently, we use boolean arrays to **remember what numbers have already appeared**.

---

## Approach
1. Create three `9 x 9` boolean arrays:
   - `rowHasNumber[row][digit]`
   - `columnHasNumber[column][digit]`
   - `subBoxHasNumber[box][digit]`

2. Traverse the board cell by cell.
3. Ignore empty cells (`'.'`).
4. Convert the digit character (`'1'–'9'`) into a `0–8` index.
5. Compute the 3×3 sub-box index using:

subBoxIndex = (row / 3) * 3 + (column / 3)

6. If the number already exists in the current row, column, or box → return `false`.
7. Otherwise, mark the number as seen.
8. If the entire board is scanned without conflicts → return `true`.

---

## Example

### Input

[
["5","3",".",".","7",".",".",".","."],
["6",".",".","1","9","5",".",".","."],
[".","9","8",".",".",".",".","6","."],
["8",".",".",".","6",".",".",".","3"],
["4",".",".","8",".","3",".",".","1"],
["7",".",".",".","2",".",".",".","6"],
[".","6",".",".",".",".","2","8","."],
[".",".",".","4","1","9",".",".","5"],
[".",".",".",".","8",".",".","7","9"]
]


### Output

true


---

## Code
```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        boolean[][] rowHasNumber = new boolean[9][9];
        boolean[][] columnHasNumber = new boolean[9][9];
        boolean[][] subBoxHasNumber = new boolean[9][9];

        for (int row = 0; row < 9; row++) {
            for (int column = 0; column < 9; column++) {
                char currentCell = board[row][column];

                if (currentCell == '.') continue;

                int digitIndex = currentCell - '0' - 1;
                int subBoxIndex = (row / 3) * 3 + (column / 3);

                if (rowHasNumber[row][digitIndex] ||
                    columnHasNumber[column][digitIndex] ||
                    subBoxHasNumber[subBoxIndex][digitIndex]) {
                    return false;
                }

                rowHasNumber[row][digitIndex] = true;
                columnHasNumber[column][digitIndex] = true;
                subBoxHasNumber[subBoxIndex][digitIndex] = true;
            }
        }
        return true;
    }
}

Time Complexity

O(1)

(The board size is fixed at 9×9.)
Space Complexity

O(1)

(Uses fixed-size boolean arrays.)
Notes

    Boolean arrays are faster and more memory-efficient than HashSets for this problem.

    The key trick is computing the sub-box index correctly.

    Always convert digits to 0–8 before using them as array indices.

yaml
