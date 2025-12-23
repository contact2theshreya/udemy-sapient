
def payment_logic():
    print("Payment modes available is credit card, debit card and UPI")


# Use the payment logic in amazon.in
payment_logic()



# use the payment logic in primevideo
payment_logic()

def payment_details(name, address, phone):
    print("Name:", name, " Address of the user is:", address, "Phone number is: ", phone)
    print("Payment options available are credit card, debit card and UPI")

payment_details("Sanket", "A/B D-Block", 9898989898)

payment_details("Sarthak", "D-C B Block", 9999999999)

def calculate_square(num):
    print("Square value is", num * num)

calculate_square(9)

calculate_square(8)

calculate_square(18)

<img width="530" height="375" alt="image" src="https://github.com/user-attachments/assets/58274e3d-3f06-4ab0-a9c6-91bb2d10fba3" />

# with return type

def payment_details(name, address, phone):
    print("Name:", name, " Address of the user is:", address, "Phone number is: ", phone)
    return "Credit card" , "UPI"

payment_option = payment_details("Sanket", "A/B D-Block", 9898989898)

print("Available payment options are", payment_option)

def calculate_square(num):
    return num*num

result = calculate_square(7)

print("The returned square value is", result)

<img width="537" height="228" alt="image" src="https://github.com/user-attachments/assets/8cfe0e39-818d-484e-aadd-db66e282a4c2" />

#Check prime

def check_prime(num):
    for div in range(2, num):
        if num % div == 0:
            # we are sure that input num is not prime
            return False

    # if the loop completed and we never found a number to completely divide num
    return True

result = check_prime(12)
if(result == True):
    print("It is a prime")
else:

    print("It is not a prime")

# nested function

<img width="541" height="270" alt="image" src="https://github.com/user-attachments/assets/dd7c8e73-b216-4e48-b3ee-20370bd354ba" />

# scope 

<img width="497" height="232" alt="image" src="https://github.com/user-attachments/assets/1eaa34d7-2f98-4bf8-952a-b7fb54bcfe48" />

Here we can not update global price variable inside function as it will be treated as local variable

<img width="350" height="196" alt="image" src="https://github.com/user-attachments/assets/4a26dde1-8cd6-4a74-a191-85ed0b875756" />

but with this we can update using global keyword

<img width="427" height="259" alt="image" src="https://github.com/user-attachments/assets/505f1823-4774-4ced-99e4-a3179356e705" />

<img width="941" height="383" alt="image" src="https://github.com/user-attachments/assets/3e82871f-5cb0-42de-9edc-c2f5f2ef64da" />

<img width="959" height="445" alt="image" src="https://github.com/user-attachments/assets/d20cc587-9094-401a-b48a-16e75bc98abf" />


<img width="953" height="433" alt="image" src="https://github.com/user-attachments/assets/e57eb1ed-5487-465c-86a0-8553526e88c7" />

# default param

<img width="959" height="410" alt="image" src="https://github.com/user-attachments/assets/474494da-d9a3-4a30-a41a-50e88003ea12" />

default param should be at end in order

<img width="958" height="398" alt="image" src="https://github.com/user-attachments/assets/8f46457a-acdc-4bef-829c-ab09ff157136" />

<img width="607" height="263" alt="image" src="https://github.com/user-attachments/assets/a43540ca-b0a7-4560-bef1-0099d84e7f6d" />

<img width="959" height="400" alt="image" src="https://github.com/user-attachments/assets/3b1c65ba-6c76-454e-88c5-a1925db4ceca" />
