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

