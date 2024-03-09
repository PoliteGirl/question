## Complexity time and space

1. **Time Complexity:**
   Time complexity represents the amount of time an algorithm takes to complete, as a function of the size of the input. It is typically expressed using big O notation, which describes the upper bound of the growth rate of an algorithm's running time concerning the input size.

   - **Example:**
     If an algorithm has a time complexity of O(n), it means the running time grows linearly with the size of the input.

   - Common time complexities:
     - O(1): Constant time
     - O(log n): Logarithmic time
     - O(n): Linear time
     - O(n log n): Linearithmic time
     - O(n^2): Quadratic time
     - O(2^n): Exponential time
     - O(n!): Exponential time
      

2. **Space Complexity:**
   Space complexity represents the amount of memory space an algorithm requires as a function of the input size. Similar to time complexity, space complexity is also expressed using big O notation.

   - **Example:**
     If an algorithm has a space complexity of O(n), it means the memory usage grows linearly with the size of the input.

   - Common space complexities:
     - O(1): Constant space
     - O(n): Linear space
     - O(n^2): Quadratic space

   Algorithms with lower space complexity are generally more memory-efficient.

--------
## Binary search has O(logN) complexity mostly when you start from middle and go back and forth from you position and search for element it will be logn complexity.

## Supose you have one Array with element same as index and finding element from it would give O(1) time comlexity

## Table of algo complexity
Creating a comprehensive chart of time complexity for various algorithms involves considering different categories and their respective complexities. Here's a simplified chart outlining common time complexities:

| Algorithm             | Time Complexity      | Best Case           | Average Case         | Worst Case           |
| **Sorting Algorithms**|                      |                     |                      |                      |
|-----------------------|----------------------|---------------------|----------------------|----------------------|
| Bubble Sort           | O(n)                 | O(n)                | O(n^2)               | O(n^2)               |
|-----------------------|----------------------|---------------------|----------------------|----------------------|
| Selection Sort        | O(n^2)               | O(n^2)              | O(n^2)               | O(n^2)               |
|-----------------------|----------------------|---------------------|----------------------|----------------------|
| Insertion Sort        | O(n)                 | O(n)                | O(n^2)               | O(n^2)               |
|-----------------------|----------------------|---------------------|----------------------|----------------------|
| Merge Sort            | O(n log n)           | O(n log n)          | O(n log n)           | O(n log n)           |
|-----------------------|----------------------|---------------------|----------------------|----------------------|
| QuickSort             | O(n log n)           | O(n log n)          | O(n log n)           | O(n^2) (unbalanced)  |
|-----------------------|----------------------|---------------------|----------------------|----------------------|
| Heap Sort             | O(n log n)           | O(n log n)          | O(n log n)           | O(n log n)           |
|-----------------------|----------------------|---------------------|----------------------|----------------------|
| **Searching Algorithms**|                    |                     |                      |                      |
|-----------------------|----------------------|---------------------|----------------------|----------------------|
| Linear Search         | O(n)                 | O(1)                | O(n/2)               | O(n)                 |
|-----------------------|----------------------|---------------------|----------------------|----------------------|
| Binary Search         | O(log n)             | O(1)                | O(log n)             | O(log n)             |
|-----------------------|----------------------|---------------------|----------------------|----------------------|

Keep in mind that this chart provides a general overview, and there are other complexities not included here. Additionally, the choice of algorithm depends on the specific requirements and constraints of the problem at hand. In practice, developers often strive to use algorithms with lower time complexities whenever possible to achieve more efficient solutions.
