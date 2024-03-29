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

Here's a table summarizing various sorting and searching algorithms, including their time complexity, space complexity, whether they can be implemented online (i.e., process elements as they come without knowing the total number of elements in advance), and whether they are stable (i.e., maintains the relative order of equal elements):

| Algorithm         | Time Complexity (Average) | Time Complexity (Worst) | Space Complexity | Online? | Stable? |
|-------------------|----------------------------|-------------------------|------------------|---------|---------|
| **Sorting Algorithms** | | | | | |
| Bubble Sort       | O(n^2)                     | O(n^2)                  | O(1)             | Yes     | Yes     |
| Insertion Sort    | O(n^2)                     | O(n^2)                  | O(1)             | Yes     | Yes     |
| Selection Sort    | O(n^2)                     | O(n^2)                  | O(1)             | No      | No      |
| Merge Sort        | O(n log n)                 | O(n log n)              | O(n)             | No      | Yes     |
| Quick Sort        | O(n log n)                 | O(n^2) (worst case)     | O(log n)         | No      | No      |
| Heap Sort         | O(n log n)                 | O(n log n)              | O(1)             | No      | No      |
| Counting Sort     | O(n + k)                   | O(n + k)                | O(n + k)         | No      | Yes     |
| Radix Sort        | O(nk)                      | O(nk)                   | O(n + k)         | No      | Yes     |
| Bucket Sort       | O(n + k)                   | O(n^2) (worst case)     | O(n + k)         | No      | Yes     |
| **Searching Algorithms** | | | | | |
| Binary Search     | O(log n)                   | O(log n)                 | O(1)             | No      | N/A     |
| Linear Search     | O(n)                       | O(n)                     | O(1)             | Yes     | N/A     |

Note:
- "n" refers to the number of elements in the input array.
- "k" refers to the range of the input.
- "Online?" indicates whether the algorithm can process elements as they come without knowing the total number of elements in advance.
- "Stable?" indicates whether the algorithm maintains the relative order of equal elements.

Keep in mind that this chart provides a general overview, and there are other complexities not included here. Additionally, the choice of algorithm depends on the specific requirements and constraints of the problem at hand. In practice, developers often strive to use algorithms with lower time complexities whenever possible to achieve more efficient solutions.

## Example usage: Linear search
```
const arr = [5, 3, 8, 4, 2];
const target = 8;
let found = false;

for (let i = 0; i < arr.length; i++) {
    if (arr[i] === target) {
        console.log(`Element ${target} found at index ${i}.`);
        found = true;
        break; // Break out of the loop since we found the target
    }
}

if (!found) {
    console.log(`Element ${target} not found in the array.`);
}
```

## Example usage: Binary search
Only for shorted array
```
function binarySearch(arr, target) {
    let low = 0;
    let high = arr.length - 1;

    while (low <= high) {
        let mid = Math.floor((low + high) / 2);

        if (arr[mid] === target) {
            return mid; // Return the index if target is found
        } else if (arr[mid] < target) {
            low = mid + 1; // Search the right half
        } else {
            high = mid - 1; // Search the left half
        }
    }

    return -1; // Return -1 if target is not found
}

// Example usage:
const arr = [2, 3, 4, 5, 8];
const target = 8;
const result = binarySearch(arr, target);
if (result !== -1) {
    console.log(`Element ${target} found at index ${result}.`);
} else {
    console.log(`Element ${target} not found in the array.`);
}
```

### Bubble sort
```
function bubbleSort(arr) {
    const n = arr.length;
    for (let i = 0; i < n - 1; i++) {
        for (let j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j+1]
                const temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    return arr;
}

// Example usage:
const arr = [64, 34, 25, 12, 22, 11, 90];
console.log("Original array:", arr);
console.log("Sorted array:", bubbleSort(arr));
```
