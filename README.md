# Conversion of numbers into their respective word representation using Python
# Define lists for word representations
ones = ["", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine"]
teens = ["", "eleven", "twelve", "thirteen", "fourteen", "fifteen", "sixteen", "seventeen", "eighteen", "nineteen"]
tens = ["", "ten", "twenty", "thirty", "forty", "fifty", "sixty", "seventy", "eighty", "ninety"]

# Function to convert a number to words
def number_to_words(number):
    if number == 0:
        return "zero"
    
    # Split the number into thousands, millions, billions, etc.
    num_parts = []
    while number > 0:
        num_parts.append(number % 1000)
        number //= 1000
    
    # Convert each part to words
    word_parts = []
    for i, part in enumerate(num_parts):
        if part == 0:
            continue
        
        part_words = []
        
        # Convert hundreds place
        if part >= 100:
            part_words.append(ones[part // 100] + " hundred")
            part %= 100
        
        # Convert tens and ones place
        if part >= 20:
            part_words.append(tens[part // 10])
            part %= 10
        elif part >= 11:
            part_words.append(teens[part - 10])
            part = 0
        
        if part > 0:
            part_words.append(ones[part])
        
        # Add the appropriate magnitude word (thousand, million, billion, etc.)
        if i > 0:
            part_words.append(["", "thousand", "million", "billion", "trillion"][i])
        
        word_parts.append(" ".join(part_words))
    
    # Reverse and join the word parts
    word_parts.reverse()
    return " ".join(word_parts)

# Input from the user
number = int(input("Enter a number: "))
word_representation = number_to_words(number)
print(f"The word representation of {number} is: {word_representation}")
