# All about recursions

    Recursion is when a function calls itself (directly or indirectly) to solve a problem.

    The idea: 👉 Break a big problem into smaller subproblems of the same type, solve those, and combine results.

## Structure of a Recursive Solution

1. Base Case → condition that stops recursion (smallest problem we can solve directly).
    - Without this, recursion would run forever
    - This means there should be a return statement without function call

2. Recursive Case → logic where the function calls itself on a smaller input.      

## Example 1: Factorial

    Factorial of n = n * (n-1) * ... * 1.

    Recursive definition:
        Base case: fact(0) = 1
        Recursive case: fact(n) = n * fact(n-1)
    
    def factorial(n):
        if n == 0:   # base case
            return 1
        return n * factorial(n-1)   # recursive case

## Example 2: Fibonacci Numbers

    Fibonacci series: 0, 1, 1, 2, 3, 5, 8...
        Base case: fib(0)=0, fib(1)=1
        Recursive case: fib(n)=fib(n-1)+fib(n-2)

    def fibonacci(n):
        if n <= 1:   # base case
            return n
        return fibonacci(n-1) + fibonacci(n-2) # recursive case
