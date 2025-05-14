Time complexity measures the time an algorithm takes to execute, as a function of the input size(n).
Big-O notation is used to describe the worst-case complexity of an algorithm, it ignores constants and lower-order terms, focusing on asymptotic behavior (when `n` tends to infinity).

### Why is this important?
- **Scalability**: algorithms with high complexity (e.g. O(n²)) can become unfeasible for large inputs.
- **Efficiency:** Choosing the right data structure or algorithm with the correct complexity can dramatically improve performance.
- **Decision-Making:** Knowing how to analyze complexity helps in choosing the best solution for a problem.

| Structure                    | Access   | Search   | Insert   | Delete   |     |
| ---------------------------- | -------- | -------- | -------- | -------- | --- |
| **[[Array]]**                | O(1)     | O(n)     | O(n)*    | O(n)*    |     |
| **[[Linked List]]**          | O(n)     | O(n)     | O(1)**   | O(1)**   |     |
| **[[Stack]]/[[Queue]]**      | -        | -        | O(1)     | O(1)     |     |
| **[[Heap (Priority Tree)]]** | O(1)***  | -        | O(log n) | O(log n) |     |
| **[[Hashmap]]**              | O(1)     | O(1)     | O(1)     | O(1)     |     |
| **BST** ([[Trees]])          | O(log n) | O(log n) | O(log n) | O(log n) |     |
| **[[HashSet]] Set (Hash)**   | -        | O(1)     | O(1)     | O(1)     |     |
\* Insertion/removal in the middle of the array.
\** After finding the position (search O(n)).
\*** Access to the maximum/minimum element in the heap.

#### Types of Time complexity:
*Best to worst*
- **O(1) - Constant**: The execution time is fixed, regardless of the input size.
- **O(log n) - Logarithmic:** The execution time grows logarithmically with the input size.
- **O(n) - Linear:** The execution time grows proportionally to the input size.
- **O(n log n) - Linearithmic:** The execution time grows slightly faster than linear, but is sill efficient.
- **O(n²) - Quadratic:** The execution time grows quadratically with the input size.
- **O(2^n) - Exponential:** The execution time doubles with each increment in the input size.
- **O(n!) - Factorial:** The execution time grows factorially with the input size.
