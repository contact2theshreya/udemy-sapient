<img width="708" height="399" alt="image" src="https://github.com/user-attachments/assets/cea86e66-47cb-4d2b-8666-cb5ff25b3dd4" />

Here’s a **clean and simple Python solution** to check whether a number **N is in the Fibonacci sequence**.

---

## ✅ Approach 1: Using a loop (easy to understand)

```python
def is_fibonacci(n):
    if n < 0:
        return False

    a, b = 0, 1
    while a <= n:
        if a == n:
            return True
        a, b = b, a + b

    return False
```

### 🔍 How it works:

* Start with the first two Fibonacci numbers: `0` and `1`
* Generate Fibonacci numbers until the value is ≥ `n`
* If `n` matches any number → return `True`
* Otherwise → return `False`

---

### 🧪 Example

```python
print(is_fibonacci(21))  # True
print(is_fibonacci(22))  # False
print(is_fibonacci(0))   # True
print(is_fibonacci(1))   # True
```

---

## ⚡ Approach 2 (Optimized – Math-based)

A number `N` is Fibonacci **if and only if**:

[
5N^2 + 4 \quad \text{or} \quad 5N^2 - 4
]
is a **perfect square**

```python
import math

def is_fibonacci(n):
    if n < 0:
        return False

    def is_perfect_square(x):
        s = int(math.sqrt(x))
        return s * s == x

    return is_perfect_square(5*n*n + 4) or is_perfect_square(5*n*n - 4)
```

---

## 🆚 Which should you use?

| Method      | Best for             |
| ----------- | -------------------- |
| Loop method | Learning, interviews |
| Math method | Performance, large N |

If you want:

* explanation with dry run
* only for-loop version
* handling big numbers
* interview-style explanation

Just say 👍

from solution import checkMember
if __name__ == "__main__":
    n=int(input())
    if(checkMember(n)):
        print("true")
    else:
        print("false")

<img width="667" height="440" alt="image" src="https://github.com/user-attachments/assets/ef54b720-6688-47d5-9c11-43d3e7416838" />

Here’s a clear and correct solution for printing a **Fahrenheit → Celsius conversion table**.

---

### 🔹 Formula Used

[
\text{Celsius} = \frac{5}{9} \times (F - 32)
]

---

### 🔹 Approach

1. Start from **S (Start Fahrenheit)**
2. Go up to **E (End Fahrenheit)**
3. Increment by **W (Step size)**
4. For each Fahrenheit value, compute and print its Celsius equivalent
5. Use **type casting** to get integer Celsius values (as usually expected in such problems)

---

### ✅ Python Program

```python
S = int(input())
E = int(input())
W = int(input())

for F in range(S, E + 1, W):
    C = int((5 / 9) * (F - 32))
    print(F, C)
```

---

### 🔹 Sample Input

```
0
100
20
```

### 🔹 Sample Output

```
0 -17
20 -6
40 4
60 15
80 26
100 37
```

---

### 🔹 Time & Space Complexity

* **Time Complexity:** O((E − S) / W)
* **Space Complexity:** O(1)

---

If you want the **Java version** or formatting output in columns, let me know 😊
