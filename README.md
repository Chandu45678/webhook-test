import string
password = input("Enter password: ")
conditions = 0
# Minimum 8 characters
if len(password) >= 8:
    conditions += 1
# At least one digit
if any(char.isdigit() for char in password):
    conditions += 1
# At least one uppercase letter
if any(char.isupper() for char in password):
    conditions += 1
# At least one lowercase letter
if any(char.islower() for char in password):
    conditions += 1
# At least one special character
if any(char in string.punctuation for char in password):
    conditions += 1
# Strength check
if conditions == 5:
    print("Password Strength: STRONG")
elif conditions >= 3:
    print("Password Strength: MEDIUM")
else:
    print("Password Strength: WEAK")








    //
