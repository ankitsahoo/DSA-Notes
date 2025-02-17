# **Strings **

## **1. What is a String?**

A **string** is a sequence of characters, typically used to represent text. In programming, strings are fundamental data types that are used to store and manipulate text-based information such as names, sentences, or any series of characters.

### **Key Characteristics of Strings:**

- **Immutable**: In many programming languages like Python, strings are immutable, meaning once a string is created, it cannot be modified.
- **Ordered**: Strings are ordered collections of characters, meaning you can access individual characters using an index.
- **Indexing**: The first character in a string has an index of `0`, the second character has an index of `1`, and so on. Negative indexing can also be used to access characters from the end of the string.
- **Length**: The length of a string is the number of characters it contains.

------

## **2. String Representation**

In most programming languages, strings are enclosed in either **single quotes** (`'`) or **double quotes** (`"`), and sometimes **triple quotes** (`'''` or `"""`) for multi-line strings.

#### Examples:

```python
single_quote_string = 'Hello, World!'
double_quote_string = "Hello, World!"
multi_line_string = '''This is
a multi-line
string'''
```

------

## **3. String Operations**

### **(1) String Concatenation**

Concatenation is the operation of joining two or more strings together to form a new string.

#### Code:

```python
str1 = "Hello"
str2 = "World"
result = str1 + " " + str2
print(result)  # Output: "Hello World"
```

### **(2) String Length**

The `len()` function returns the number of characters in a string.

#### Code:

```python
text = "Hello"
print(len(text))  # Output: 5
```

### **(3) String Indexing**

You can access individual characters of a string using an index.

#### Code:

```python
text = "Hello"
print(text[0])  # Output: H (first character)
print(text[-1]) # Output: o (last character)
```

### **(4) String Slicing**

Slicing allows you to extract a substring from a string.

#### Code:

```python
text = "Hello, World!"
print(text[0:5])   # Output: Hello (from index 0 to 4)
print(text[7:12])  # Output: World (from index 7 to 11)
```

### **(5) String Multiplication**

You can repeat a string multiple times by multiplying it by an integer.

#### Code:

```python
text = "Hello"
print(text * 3)  # Output: HelloHelloHello
```

------

## **4. Common String Methods**

### **(1) `.lower()` and `.upper()`**

Converts the string to lowercase or uppercase.

#### Code:

```python
text = "Hello"
print(text.lower())  # Output: hello
print(text.upper())  # Output: HELLO
```

### **(2) `.strip()`**

Removes leading and trailing whitespace from a string.

#### Code:

```python
text = "  Hello World!  "
print(text.strip())  # Output: "Hello World!"
```

### **(3) `.replace()`**

Replaces a specified substring with another substring.

#### Code:

```python
text = "Hello, World!"
new_text = text.replace("World", "Universe")
print(new_text)  # Output: "Hello, Universe!"
```

### **(4) `.split()`**

Splits a string into a list of substrings based on a delimiter (default is whitespace).

#### Code:

```python
text = "Hello, World, Python"
split_text = text.split(", ")
print(split_text)  # Output: ['Hello', 'World', 'Python']
```

### **(5) `.find()`**

Finds the index of the first occurrence of a substring. Returns `-1` if not found.

#### Code:

```python
text = "Hello, World!"
print(text.find("World"))  # Output: 7
print(text.find("Python")) # Output: -1
```

------

## **5. String Formatting**

String formatting allows you to create complex strings by inserting variables or expressions into a string.

### **(1) Using f-strings (Python 3.6+)**

F-strings allow you to embed expressions inside string literals, prefixed with `f`.

#### Code:

```python
name = "Alice"
age = 25
greeting = f"Hello, my name is {name} and I am {age} years old."
print(greeting)  # Output: "Hello, my name is Alice and I am 25 years old."
```

### **(2) Using `.format()` Method**

This method is used in older versions of Python for string formatting.

#### Code:

```python
name = "Alice"
age = 25
greeting = "Hello, my name is {} and I am {} years old.".format(name, age)
print(greeting)  # Output: "Hello, my name is Alice and I am 25 years old."
```

### **(3) Using `%` Formatting**

This is an older style of formatting strings using `%` operators.

#### Code:

```python
name = "Alice"
age = 25
greeting = "Hello, my name is %s and I am %d years old." % (name, age)
print(greeting)  # Output: "Hello, my name is Alice and I am 25 years old."
```

------

## **6. String Searching and Matching**

### **(1) `.in` Operator**

The `in` operator checks if a substring exists within a string.

#### Code:

```python
text = "Hello, World!"
print("Hello" in text)  # Output: True
print("Python" in text) # Output: False
```

### **(2) `.startswith()` and `.endswith()`**

These methods check if a string starts or ends with a given substring.

#### Code:

```python
text = "Hello, World!"
print(text.startswith("Hello"))  # Output: True
print(text.endswith("World!"))  # Output: True
```

------

## **7. Advanced String Operations**

### **(1) Palindrome Check**

A **palindrome** is a word, phrase, or number that reads the same forward and backward. You can check if a string is a palindrome by comparing it to its reversed version.

#### Code:

```python
def is_palindrome(s):
    return s == s[::-1]

print(is_palindrome("madam"))  # Output: True
print(is_palindrome("hello"))  # Output: False
```

### **(2) Anagram Check**

Two strings are **anagrams** if they contain the same characters in any order. You can check if two strings are anagrams by sorting both strings.

#### Code:

```python
def are_anagrams(s1, s2):
    return sorted(s1) == sorted(s2)

print(are_anagrams("listen", "silent"))  # Output: True
print(are_anagrams("hello", "world"))    # Output: False
```

------

## **8. Summary of String Operations**

| **Operation**              | **Description**                                            | **Example**                                    |
| -------------------------- | ---------------------------------------------------------- | ---------------------------------------------- |
| **Concatenation (`+`)**    | Join two or more strings.                                  | `"Hello" + " " + "World"`                      |
| **Length (`len()`)**       | Return the length of the string.                           | `len("Hello")` → 5                             |
| **Slicing (`[:]`)**        | Extract a substring from the string.                       | `"Hello"[1:4]` → `"ell"`                       |
| **Upper/Lower**            | Convert the string to uppercase or lowercase.              | `"hello".upper()` → `"HELLO"`                  |
| **Find (`.find()`)**       | Find the index of a substring.                             | `"hello".find("l")` → 2                        |
| **Replace (`.replace()`)** | Replace a substring with another substring.                | `"hello".replace("l", "r")`                    |
| **Split (`.split()`)**     | Split the string into a list based on a delimiter.         | `"Hello World".split()` → `["Hello", "World"]` |
| **Join (`.join()`)**       | Join elements of a list into a string.                     | `" ".join(["Hello", "World"])`                 |
| **Starts/Ends with**       | Check if the string starts or ends with a given substring. | `"Hello".startswith("He")` → True              |

------

In summary, strings are an essential data type used in programming to handle and manipulate text. Through various built-in methods and operations, strings can be easily modified, analyzed, and formatted.