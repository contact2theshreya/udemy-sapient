<img width="958" height="416" alt="image" src="https://github.com/user-attachments/assets/dce9e017-917f-4e1a-b881-615449c3f5e1" />

<img width="884" height="407" alt="image" src="https://github.com/user-attachments/assets/c459a23e-3463-47ea-9527-edf159a2ea7e" />

<img width="920" height="465" alt="image" src="https://github.com/user-attachments/assets/3f5cd152-9c41-4051-bca9-c9f9b5605953" />

Here is a simple Python program to print the **Fahrenheit to Celsius conversion table** using **type casting** as hinted.

### Formula

[
C = \frac{5}{9} \times (F - 32)
]

---

### Python Program

```python
# Take input values
S = int(input("Enter Start Fahrenheit value: "))
E = int(input("Enter End Fahrenheit value: "))
W = int(input("Enter Step Size: "))

# Print conversion table
for F in range(S, E + 1, W):
    C = int((5 / 9) * (F - 32))   # type casting to int
    print(F, C)
```

---

### Example Input

```
Enter Start Fahrenheit value: 0
Enter End Fahrenheit value: 100
Enter Step Size: 20
```

### Output

```
0 -17
20 -6
40 4
60 15
80 26
100 37
```

---

### Explanation

* The loop increments Fahrenheit values by `W`
* Celsius is calculated using the formula
* `int()` is used to **type cast** the Celsius value (truncate decimals)
* Each line prints:
  **Fahrenheit  Celsius**

Let me know if you want the output formatted in columns or explained with a dry run 😊


<img width="959" height="454" alt="image" src="https://github.com/user-attachments/assets/64f0e165-6972-4620-af3e-69c5bb24e06f" />

<img width="349" height="281" alt="image" src="https://github.com/user-attachments/assets/80f9e5b7-2527-4f26-af22-e08d604e25c7" />
