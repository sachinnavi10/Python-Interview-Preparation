# Day-2 Python Interview Programming Questions

## 1. Reverse a String

This solution walks through the string from the last character to the first,
without using a built-in reverse function.

```python
def reverse_string(text):
    result = ""
    for index in range(len(text) - 1, -1, -1):
        result += text[index]
    return result


print(reverse_string("Python"))  # nohtyP
```

## 2. Palindrome Number

Reverse the digits and compare them with the original number. Negative numbers
are not considered palindromes.

```python
def is_palindrome(number):
    if number < 0:
        return False

    original = number
    reversed_number = 0

    while number > 0:
        digit = number % 10
        reversed_number = reversed_number * 10 + digit
        number //= 10

    return original == reversed_number


print(is_palindrome(12321))  # True
print(is_palindrome(12345))  # False
```

## 3. Find the Largest Number

Keep track of the largest value seen while iterating through the list, without
using `max()`. An empty list raises `ValueError`.

```python
def find_largest(numbers):
    if not numbers:
        raise ValueError("numbers must not be empty")

    largest = numbers[0]
    for number in numbers[1:]:
        if number > largest:
            largest = number
    return largest


print(find_largest([12, 45, 7, 32]))  # 45
```

## 4. Count Vowels

Count each occurrence of `a`, `e`, `i`, `o`, or `u`, regardless of letter case.

```python
def count_vowels(text):
    vowels = "aeiou"
    count = 0

    for character in text.lower():
        if character in vowels:
            count += 1
    return count


print(count_vowels("Interview"))  # 4
```

## 5. Factorial of a Number

Calculate the factorial using a function and a loop. The factorial of `0` is
`1`; negative inputs raise `ValueError`.

```python
def factorial(number):
    if number < 0:
        raise ValueError("number must be non-negative")

    result = 1
    for value in range(2, number + 1):
        result *= value
    return result


print(factorial(5))  # 120
```