#password_analyzer.py
from zxcvbn import zxcvbn
import math

print("======================================")
print(" PASSWORD SECURITY ANALYZER")
print("======================================")

# Password Analysis
password = input("\nEnter a fake test password: ")

result = zxcvbn(password)

charset = 0

if any(c.islower() for c in password):
    charset += 26

if any(c.isupper() for c in password):
    charset += 26

if any(c.isdigit() for c in password):
    charset += 10

if any(not c.isalnum() for c in password):
    charset += 32

if charset > 0:
    entropy = len(password) * math.log2(charset)
else:
    entropy = 0

print("\n--- Password Analysis ---")
print("Length:", len(password))
print("Score:", result["score"], "/ 4")
print("Estimated guesses:", result["guesses"])
print("Entropy:", round(entropy, 2), "bits")

if result["score"] <= 1:
    print("Strength: WEAK")
elif result["score"] == 2:
    print("Strength: FAIR")
elif result["score"] == 3:
    print("Strength: STRONG")
else:
    print("Strength: VERY STRONG")


# Custom Wordlist Generator
print("\n--- Custom Wordlist ---")

name = input("Enter dummy name: ").strip()
pet = input("Enter dummy pet name: ").strip()
year = input("Enter dummy year: ").strip()

words = set()

words.add(name)
words.add(name.lower())
words.add(name.upper())

words.add(pet)
words.add(pet.lower())
words.add(pet.upper())

words.add(year)

if name and year:
    words.add(name + year)

if pet and year:
    words.add(pet + year)

with open("custom_wordlist.txt", "w") as file:
    for word in sorted(words):
        file.write(word + "\n")

print("\nWordlist created successfully!")
print("Total entries:", len(words))
print("Saved as: custom_wordlist.txt")

print("\n======================================")
print(" PROJECT COMPLETED SUCCESSFULLY")
print("======================================")