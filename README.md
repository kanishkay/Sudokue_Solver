# 🧩 Sudoku Solver - Constraint Satisfaction Problem (CSP)


📐 A Python implementation of a Sudoku solver modeled as a Constraint Satisfaction Problem (CSP). Two approaches are compared — plain backtracking search and backtracking enhanced with AC-3 arc consistency inference — to evaluate the efficiency gained through constraint propagation.

📁 Project Structure
sudoku_solver.ipynb: Jupyter notebook containing the complete CSP formulation, solver implementations, grid visualization, and performance comparison between both approaches.

📝 CSP Formulation
Variables:
Each of the 81 cells (i, j) in the 9×9 grid is a variable, where i is the row and j is the column (0–8).
States:
Each state is a 9×9 2D list. A value of 0 represents an unassigned cell.
Domains:

Filled cells have a fixed domain containing only their given value.
Empty cells start with domain {1–9} minus all values already present in the same row, column, or 3×3 box.

Constraints:
Two cells conflict if they are in the same row, column, or 3×3 box and share the same value.

Row: All 9 values in each row must be distinct.
Column: All 9 values in each column must be distinct.
Box: All 9 values in each 3×3 sub-grid must be distinct.


📈 Key Implementation Details
Grid Visualization:

Rendered the 9×9 Sudoku board using Matplotlib's imshow with alternating shading for 3×3 boxes.
AddAssignment overlays digit values onto the grid for both the initial puzzle and the final solution.

Domain Initialization:

Computed legal domains for all 81 cells upfront using initialize_domains.
Used set operations to subtract row, column, and box values from {1–9} for each empty cell.

Backtracking Search:

Variable selection: left-to-right, top-to-bottom scan for the first empty cell.
Value ordering: tries values 1–9 in order.
Backtracks by resetting grid[i][j] = 0 when all values in a cell fail.

AC-3 Arc Consistency:

After each assignment, AC_3 propagates domain reductions to all neighbors of the assigned cell.
revise(Xi, Xj) removes any value from Xi's domain that is inconsistent with Xj's forced value.
Domains are saved via deepcopy before each AC-3 call and fully restored on backtrack to prevent domain leakage between branches.
Returns False early if any domain becomes empty, pruning that branch immediately.


📊 Results
Backtracking:           2714 assignments
Backtracking with AC-3: 46 assignments
Solutions match: True
Backtracking with AC-3 requires significantly fewer assignments by detecting dead ends early through domain propagation, demonstrating the efficiency gain of inference-based search over naive backtracking.

🛠️ Tools and Libraries Used
Python: Base language for all solver logic and visualization.
Key Libraries:

matplotlib and numpy: Sudoku grid rendering and matrix operations.
collections.deque: Queue structure for AC-3 arc processing.
copy: Deep copying domain state for safe backtracking and domain restoration.


📫 Contact: www.linkedin.com/in/kanishkayadvv
Author: Kanishka Yadav
