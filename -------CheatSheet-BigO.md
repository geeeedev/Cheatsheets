## Purpose: Notes on Understanding Big O Notation 

[Complete Guide to Big O Notaion](https://www.youtube.com/watch?v=kS_gr2_-ws8)

### Speed (Faster) - Time Complexity
- analyze the runtime of an algo as the size of the input increases
- how to evaluate: 
   - count the number of operations
      - do we have the same *number* of operations as the data grows? (simple equation)
      - in a loop, the bigger the data, the MORE operations there are - number of operations grow proportionally with n

- O(f(n)) - the number of simple operations the computer has to do 
   - O(1) 
      - always performs the x number of operations as the data grows - flat line on x-axis
      - "constant time"
      - For it to be constant time, it has to know immediately where to go and get that data.
   - O(n) 
      - number of operations is bounded by a multiple of n.  i.e., as n grows, so does number of operations
      - if one loop operation processes an array of 8 items, and there are 2 opearations for each item, there will be 16 operations total (multiple of 8 ~~ 2n where 2 ops of n times which is 8 times)
      - one for loop is 0(n)
      - diagnal linear slope 
      - "linear time"
   - O(n2) ("O of n-square")
      - n number of operations inside each of the n operations
      - a for loop *inside* a for loop is O(n2)
      - O(n) inside O(n) = O(n * n) = O(n2)
      - "quaradic time"
      - diagnal slope curving up along y-axis, gets steeper and straighter as data grows - meaning slower
      - avoid writing code that will result in O(n2) if at all possible
      - eg. Bubble Sort, Selection Sort, Insertion Sort
   - O(log n)
      - close to O(1)'s constant time flat line
      - reduce the remaining pool of values by half for each value read through
      - eg. Binary Search, Merge Sort
   - O(nlog n)
      - close to o(n2)'s very steep diagnal slope
      - employ a divide and conquer approach
      - "quick" for "worst" case scenarios
      - eg. Quick Sort

- rules of thumb (also consequences of definition of Big O)
   - Arithmetic operations ae constant
   - Variable assignment is constant
   - Accessing elements in an array (by index) or object (by key) is constant
   - In a loop, the complexity is the length of the loop (n multiple ~ O(n)) times the complexity of whatever happens inside the loop
      - so that's why if there is a nested loop inside, it becomes O(n2)



### Less memory-intensive - Space Complexity
- analyze the additional memory needed to allocate in order to run the code


### Code Readability ?
