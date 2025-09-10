# All About Big-O 

    Big O notation describes an algorithm's worst-case time or space complexity, showing how its performance scales with increasing input size. It provides an upper bound for the algorithm's growth rate, not an exact measurement, and helps compare the efficiency of different algorithms. 

    - O(1) - Constant Time: The algorithm takes the same amount of time regardless of the input size
    - O(log n) - Logarithmic Time: The runtime increases very slowly as the input size grows, such as in a binary search. 
    - O(n) - Linear Time: The runtime grows proportionally to the input size
    - O(n log n) 
    - O(n²) - Quadratic Time: The runtime grows with the square of the input size, often seen in nested loops
    
    O(1) < O(log n) < O(n) < O(n log n) < O(n²) 

## How does logarithmic time scale ? 

    Finding a number in logarithmic time, often expressed as O(log n), typically refers to algorithms like binary search. This efficiency arises from a strategy of repeatedly dividing the search space in half.

    Repeated halving leads to a logarithmic relationship between the number of elements (n) and the number of operations required.
        If you have 'n' elements, after one comparison, you have 'n/2' elements left
        After two comparisons, you have 'n/4' elements left
        After 3 comparisons, you have 'n/8' elements left
        After 'k' comparisons, you have 'n / 2^k' elements left

    The search continues until only one element is left (or the element is found). This means 'n / 2^k = 1', which simplifies to 'n = 2^k'. To find 'k', you take the logarithm base 2 of both sides: 'log₂(n) = k'.

    Therefore, the number of operations 'k' required in the worst case is proportional to log₂(n). This is why finding a number using an efficient algorithm like binary search in a sorted dataset has a time complexity of O(log n). The base of the logarithm is often omitted in Big O notation because it only changes the constant factor and not the fundamental growth rate of the algorithm.

## 