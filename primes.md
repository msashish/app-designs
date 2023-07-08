# Importance of Prime numbers

## Basics

    1. Prime number is a number that cannot be divisible by any other number but itself and 1. 
        - This removes half of the numbers in universe (evens) and multiples of other numbers 
        - If you take a big number and start distributing it or keep dividing it then the lowest set of numbers that 
        we get which cannot be divided further are primes.

    2. Prime numbers are the building blocks of all numbers in the universe.
        - Take any number, and it can be expresed as a multiple of prime numbers
            155 = 5 * 31
            90  = 2 * 3 * 3 * 5
            12 = 2 * 2 * 3
        - Having prime numbers is enough to construct all numbers in the universe
        - All numbers in the universe = Multiples of Prime numbers

    3. (Sad) There are infinite prime numbers. They become less frequent as we go towards infinity.

## In Cryptography

    Special properties of factorization:
        It is relatively easy to find larger prime numbers but its very hard to factor large numbers back into primes. 
        There just doesnt seem to be any efficient way to factor large numbers. 

        - To figure out prime factors for 2244354 will take a lot of time and computation
            2244354 = 2 * 3 * 7 * 53437
        - This is what makes it vital for communications, modern computer crypography
        - Super computer could chew on a 256-bit factorization problem for longer than the age of universe and still not get the answer !!

    But how is it used in computer crypography ?
        Consider a Lock and a Key scenario. Lock can be seen by public but no one can open it without a key. 
        A large number 2244354 is uniquely related to its Prime factors [2, 3, 7, 53437].
        Computer crypography uses large number as Lock (public) while its Prime factors as key (private)
            - A file can be encrypted using large number 2244354 which can be publicly shared
            - Cryptographic encryption algorithm ensures that such a file can only be decrypted using its prime factors [2, 3, 7, 53437] which 
                are private and not publicly shared
            - If a hacker gets 2244354, its extremely hard to get [2, 3, 7, 53437] or with changed order. 256-bit factorization problem is uncrackable.


