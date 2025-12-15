num = 1

while num <= 10:
    # body of the while loop
    print(num)
    num += 1

print("Ending the program")

# sum of no

num = 1
N = int(input()) # this is a user input
s = 0 # this will store our final sum

while num <= N:
    print(s, num)
    s += num # whatever is the current natural number, add it to s
    num += 1 # move to the next natural number

# when the loop ends, print s
print(s)

# sum of even number

<img width="637" height="415" alt="image" src="https://github.com/user-attachments/assets/28870284-2833-43a2-a087-54b7fe7a4205" />


N =int(input())
s=0
i=2
while i<=N:
    s += i
    i += 2;
 
print(s)


# print only even natural number 

num = 1

while(num <= 10):
    if num % 2 != 0:
        # num is odd
        num += 1 # go to the next natural number
        continue # go to the nearest loop again
    print(num)
    num += 1

num = 1

# print till 20 except 13
while(num <= 20):
    if num == 13:
        print("stopping the loop here....")
        break # stop the nearest loop
    print(num)
    num += 1

print("End")
# pass -showing an empty sttement and we will add lines later

num = 1

while(num <= 20):
    if num == 13:
        pass
    print(num)
    num += 1

print("End")

<img width="668" height="347" alt="image" src="https://github.com/user-attachments/assets/1b82fd50-0e8c-4d02-9c7a-83a64bca0eae" />

<img width="959" height="395" alt="image" src="https://github.com/user-attachments/assets/2605a5d2-764c-493c-9d13-726062e1b9a0" />

