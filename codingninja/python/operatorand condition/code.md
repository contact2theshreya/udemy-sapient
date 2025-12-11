# Largest of 3 no


x=  int(input())
y=  int(input())
z=  int(input())
if x>y and x>z:
    print(x)
elif y>x and y>z:
    print(y)
else:
    print(z)
# nested if


x = int(input())

if x >= 0:
    # this number will be either positive or zero
    if x == 0:
        print("Zero")
    else:
        print("Positive")
else:
    # this number is negative
    if x < -500:
        print("Too much negative")
    else:
        print(" Just Negative")

# Ternary operator

print("hello") if 10 < 2 else print("no hello")
