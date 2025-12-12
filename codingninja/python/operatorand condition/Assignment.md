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
