# AI: Assignment 1

## Parts

- Question 1: Introduction
- Question 2: Agenda-based search
- Question 3: Evolutionary computing

## Mistakes or inadequecies in the final submission

1.<br>
The last point of question 2.2 was misinterpreted by me. Reverse order of nodes explored per level means that the order in which the children of a node must be explored must be reversed. Instead, I interpreted it as the inverse order of the end states (initial and goal).
<br><br>2.<br>
The line cost is considered as follows: if no line change occurs, do the usual cost evaluation, else if line change occurs, add 2 to the usual cost evaluation. Although this is stated and implied in the code and comments, it is still not adequately clear in the section where this question needs to be addressed.
