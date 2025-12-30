<img width="937" height="449" alt="image" src="https://github.com/user-attachments/assets/9a6c866e-1405-4842-9adb-c3ea6ddc5bb9" />

<img width="959" height="415" alt="image" src="https://github.com/user-attachments/assets/42123f71-9b64-4ba9-8f75-c0ae8059b30c" />

<img width="959" height="467" alt="image" src="https://github.com/user-attachments/assets/ddd7fd02-e5a2-48c8-863b-d1082a0c7575" />

# slicing - to access any piece of arrauy(non immutable)

<img width="308" height="195" alt="image" src="https://github.com/user-attachments/assets/c618b376-043d-4cdd-8fe4-0bca080e79ed" />

<img width="458" height="199" alt="image" src="https://github.com/user-attachments/assets/ee0bab98-948b-421a-a78a-5a90b3b42f31" />

<img width="433" height="236" alt="image" src="https://github.com/user-attachments/assets/c91a293b-d4f7-4b9c-8826-3e4de0ac9337" />

<img width="268" height="137" alt="image" src="https://github.com/user-attachments/assets/9700adad-e324-4f4f-9b7d-dbced7d1dd3c" />

<img width="547" height="349" alt="image" src="https://github.com/user-attachments/assets/77b3497a-e70b-45c0-91af-77acde5e8b78" />

<img width="560" height="275" alt="image" src="https://github.com/user-attachments/assets/6d4202f4-ace9-4588-9124-cde5240b35cb" />

<img width="683" height="350" alt="image" src="https://github.com/user-attachments/assets/7fd6217e-0497-4ea7-8982-dc632cdb96f3" />

# swap alternate pair

<img width="245" height="169" alt="image" src="https://github.com/user-attachments/assets/ee67cd81-14e5-4de2-a0f3-5b5d0eec45ad" />

# rearrange no

all even should come first then odd will come at last

use pointer to arrange inplace

<img width="839" height="347" alt="image" src="https://github.com/user-attachments/assets/5cf8679b-9bfc-4c2a-a3a5-4d69c8ca0219" />

<img width="713" height="428" alt="image" src="https://github.com/user-attachments/assets/4bca3d02-2581-4a01-bdb6-0538f0ed24a3" />

# count pair sum

<img width="921" height="425" alt="image" src="https://github.com/user-attachments/assets/8f5fc937-ab9c-441c-b3a1-8d71d99e331b" />

# triiplet sum

Below is the **Triplet Sum using only `for` loops**, explained **step-by-step for a beginner**.

---

## 🔹 Problem (Triplet Sum)

Given an array `ARR` of size `N` and a value `X`,
find the **number of triplets** `(i, j, k)` such that:

```
ARR[i] + ARR[j] + ARR[k] == X
```

and

```
i < j < k
```

---

## ✅ Solution Using **Only `for` Loops** (Brute Force)

```python
def tripletSum(arr, n, x):
    count = 0

    for i in range(n):
        for j in range(i + 1, n):
            for k in range(j + 1, n):
                if arr[i] + arr[j] + arr[k] == x:
                    count += 1

    return count
```

---

## 🔍 Explanation (Beginner Friendly)

### Why **three for loops**?

Because:

* We need **3 different elements**
* Every possible combination must be checked

---

### Loop Structure

```python
for i in range(n):          # first element
    for j in range(i+1, n):# second element
        for k in range(j+1, n): # third element
```

✔ Ensures `i < j < k`
✔ No duplicate triplets
✔ No same element used twice

---

## 🔹 Example Dry Run

```python
arr = [1, 2, 3, 4, 5]
x = 9
```

Valid triplets:

```
(1,3,5) → 1+3+5 = 9
(2,3,4) → 2+3+4 = 9
```

✅ Output:

```
2
```

---

## ⏱ Complexity

| Type  | Value     |
| ----- | --------- |
| Time  | **O(N³)** |
| Space | **O(1)**  |

---

## ❌ Common Beginner Mistakes

### ❌ Wrong loop start

```python
for j in range(n):  # WRONG
```

✔ Should start from `i+1`

---

### ❌ Reusing same index

```python
if arr[i] + arr[i] + arr[k] == x  # WRONG
```

---

## 🧠 When is this approach acceptable?

✔ Small constraints
✔ Learning basics
✔ Coding interviews (first solution)

---

## ⭐ Interview Tip

> Always start with brute force using loops,
> then mention optimized approach if asked.

---

If you want next:

* Optimized **O(N²)** approach
* Handling **duplicate elements**
* Triplet sum in **sorted array**
* Java / C++ version

Just tell me 👍

