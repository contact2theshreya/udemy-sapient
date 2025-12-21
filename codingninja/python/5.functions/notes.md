
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
