# Crossword Optimizer


## Background:

Given the structure of a crossword puzzle:
* which squares of the grid are to be filled with letters
* which sequence of squares belong to which word to be filled in
* the direction of each word - across or down - in the puzzle
and a list of words to use, the problem of generating a crossword pizzle is choosing which words should go in each sequence of squares.

Each sequence of squares can be is one variable, the value of which needs to be decided from a domain of possible words that will fill the sequence.

These variables have both unary and binary constraints:
* The unary constraint on a variable is its length, i.e. a variable with 4 spaces to be filled in can only accept 4-letter words as values. Any values that do not satisfy a variable's unary constraints can be removed from the variable's domain immediately (enforcing node consistency).
* The binary constraints on a variable are given if its squares overlap with another variable. For example if variable 1 and variable 2 are both consist of four blank spaces and overlap such that variable 1's second space is variable 2's first space, the second character of variable 1's value is constrained to be the same as the 1st character of variable 2's value. Enforcing arc consistency on these variables would result in removing any options from one variable that would not have a corresponding option in one of its constrained variables.
* A further constraint for this specific problem is that all words in the puzzle must be different. This can be formalised as an additional set of binary constraints between every pair of variables such that no two variables can be the same value.

### Node Consistency

* Node Consistency - when all the values in a viarbles domain satisfy the variable's unary constraints.

### Arc Consistency

* Arc Consistency - when all the values in a variable's domain satisfy the variable's binary constraints.
* To make X arc-consistent with respect to Y, remove elements from X's domain until every choice for X has a possible choice for Y.
  
### Backtracking Search

* Backtracking Search is a recursive algorithm often employed to solve constraint satisfaction problems. Here values are assigned to each variable from the variable's domain, one at a time.
  * If the assignment is consistent with the conditions of the problem being solved, Backtracking Search is recursively called on the csp until all variables are assigned. If all variable are successfully assigned, the problem has been solved and the solution is returned.
  * If a variable is unable to be assigned consistently, the algorithm then returns to a previous variable and changes its assignment to another from its domain, until all options are exhausted. If all options for all variables are exhausted and no solution found, there is no solution to the csp.
* Pseudocode for a backtracking search algorithm is:

## Usage:

Requires Python(3) to run, and installation of Pillow if output images are desired, which can be done via `pip install pillow`.

To run standard backtracking search:
$python(3) generate.py data/structureX.txt data/wordsX.txt False [output_image_filename.png]

To run backtracking search with interleaved arc consistency enforcement:
$python(3) generate.py data/structureX.txt data/wordsX.txt True [output_image_filename.png]


