<img width="959" height="446" alt="image" src="https://github.com/user-attachments/assets/dc66eb45-035f-4b0e-b886-d40b67c3e2bb" />

<img width="956" height="403" alt="image" src="https://github.com/user-attachments/assets/7d330396-7b3c-4c05-af0f-db0f30847d50" />

In Python, **there’s no direct `input()` that returns a boolean**, because `input()` always returns a **string**. You need to **convert the input** to a boolean manually. Here’s how you can do it:

---

## **1. Using simple string comparison**

```python
user_input = input("Enter True or False: ")
bool_value = user_input.strip().lower() == "true"

print(bool_value, type(bool_value))
```

**Example:**

```
Enter True or False: True
Output: True <class 'bool'>

Enter True or False: false
Output: False <class 'bool'>
```

✅ Works for `True`/`False` strings (case-insensitive).

---

## **2. Using a helper function**

```python
def str_to_bool(s):
    if s.lower() in ["true", "t", "yes", "1"]:
        return True
    elif s.lower() in ["false", "f", "no", "0"]:
        return False
    else:
        raise ValueError("Invalid boolean input")

user_input = input("Enter a boolean value: ")
bool_value = str_to_bool(user_input)

print(bool_value)
```

**Example:**

```
Enter a boolean value: yes
Output: True
```

---

## **3. Using `distutils.util.strtobool` (built-in method)**

```python
from distutils.util import strtobool

user_input = input("Enter a boolean value: ")
bool_value = bool(strtobool(user_input))  # Returns 0 or 1, convert to bool
print(bool_value)
```

**Valid inputs:**

* `"y"`, `"yes"`, `"t"`, `"true"`, `"on"`, `"1"` → `True`
* `"n"`, `"no"`, `"f"`, `"false"`, `"off"`, `"0"` → `False`

---

💡 **Tip:** Always normalize the input (`.strip().lower()`) to handle extra spaces or different cases.

---

If you want, I can also **show how to take multiple boolean inputs at once from a single line**, like `[True, False, True]`.

Do you want me to show that?

<img width="794" height="412" alt="image" src="https://github.com/user-attachments/assets/8d35b68d-e48e-4e7b-a8fc-27e62e24cd63" />

<img width="959" height="442" alt="image" src="https://github.com/user-attachments/assets/ad2cd092-ab34-4487-93ab-8f1b0d1962ef" />

<img width="959" height="453" alt="image" src="https://github.com/user-attachments/assets/a9f5a305-0f47-490a-aa3c-49f14da539f4" />

<img width="708" height="382" alt="image" src="https://github.com/user-attachments/assets/bb4c5372-b609-4d16-a7ec-d9a758be5ace" />

Total Salary
Problem Description: You have to calculate the rounded off total salary of a person by using
the formula: totalSalary = basic + hra + da + allow – pf, where hra = 20% of basic, da = 50% of
basic, allow = 1700, if grade = ‘A’, allow = 1500, if grade = ‘B’, allow = 1300, if grade = ‘C' or
any other character, pf = 11% of basic. “basic” and the “grade” will be taken as input from the
user.
How to Approach?
1. Take basic and grade as input from the user.
2. Calculate hra, da, pf by using basic.
3. Check for the grade and then take the allowance corresponding to it.
4. Calculate total salary by using basic, hra, da, pf and allowance calculated above.
5. Round off the total salary using library function and then print it.
Pseudo Code for this problem:
input=basic
input=grade
hra = 0.2 * basic
da = 0.5 * basic
if(grade == 'A') :
 allowance = 1700
else if(grade == 'B') :
 allowance = 1500
 else :
 allowance = 1300
pf = 0.11 * basic
totalSalary = basic + hra + da + allowance - pf
ans = round(totalSalary)
print(ans)
❏ Let us dry run the code:
basic=10000
grade= ‘A’
● hra=0.2*10000=2000
● da=0.5*10000=5000
● Now, we have grade=’A’, so allowance=1700
● pf=0.11*10000=1100
● Total salary=10000+2000+5000+1700-1100=17600
● Rounding off will keep it 17600 which is our output print it.
