# Artificial Intelligence Nanodegree
## Introductory Project: Diagonal Sudoku Solver

# Question 1 (Naked Twins)
Q: How do we use constraint propagation to solve the naked twins problem?  
A: 1) First step is to find if 2 boxes in a unit have exactly the same pair of digits as values. Copying a snippet from the code. 
    pairs = [s + t for s in  digits for t in digits if s!=t]
    
    for unit in unitlist:
        for pair in pairs:
            dplaces = [box for box in unit if values[box] == pair]
            if len(dplaces) == 2:
                boxes_to_replace = [box_temp for box_temp in unit if box_temp not in dplaces] ---> This holds the boxes with naked twins
		
   2) Once we find that, we go through all the remaining boxes in the unit, and remove both the digits if present - thus propagating the constraint.  Again following is the code snippet :
   boxes_to_replace = [box_temp for box_temp in unit if box_temp not in dplaces]
   for box_temp in boxes_to_replace :
         value = values[box_temp]
         values[box_temp] = ''.join(temp for temp in value if temp not in pair) --> Remove digits in other boxes part of the twins. 

# Question 2 (Diagonal Sudoku)
Q: How do we use constraint propagation to solve the diagonal sudoku problem?  
A: 1) Create a separate data structure (list of list) for holding the 2 diagonal units - each diagonal unit has 9 boxes.
   diag_units = []
   diag_units.append([rows[i]+cols[i] for i in range(0,len(rows))])
   diag_units.append([rows[::-1][j]+cols[j] for j in range(0,len(rows))])

   2) For each of the 2 diagonal unit, use elimination, only_choice and naked_twins technique to figure out constraints for each boxes and propagate to whole unit. 
      
### Install

This project requires **Python 3**.

We recommend students install [Anaconda](https://www.continuum.io/downloads), a pre-packaged Python distribution that contains all of the necessary libraries and software for this project. 
Please try using the environment we provided in the Anaconda lesson of the Nanodegree.

##### Optional: Pygame

Optionally, you can also install pygame if you want to see your visualization. If you've followed our instructions for setting up our conda environment, you should be all set.

If not, please see how to download pygame [here](http://www.pygame.org/download.shtml).

### Code

* `solutions.py` - You'll fill this in as part of your solution.
* `solution_test.py` - Do not modify this. You can test your solution by running `python solution_test.py`.
* `PySudoku.py` - Do not modify this. This is code for visualizing your solution.
* `visualize.py` - Do not modify this. This is code for visualizing your solution.

### Visualizing

To visualize your solution, please only assign values to the values_dict using the ```assign_values``` function provided in solution.py

### Data

The data consists of a text file of diagonal sudokus for you to solve.