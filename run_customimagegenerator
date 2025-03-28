import hashlib
from PIL import Image, ImageDraw
import random

def generate_pattern(birth_date, favorite_color, license_plate):
    # convert birth date to a number (e.g., DDMMYYYY)
    birth_date_number = int(birth_date.replace("-", ""))  # format: YYYY-MM-DD

    # conver favorite color (hex or RGB) to a numeric value
    color_value = int(favorite_color.lstrip('#'), 16)  # convert hex color to an integer

    # license plate number (convert to a sum of ASCII values)
    license_plate_value = sum(ord(c) for c in license_plate)

    # combine all the values in a creative way using a hash function
    combined_value = birth_date_number + color_value + license_plate_value
    unique_pattern_seed = hashlib.sha256(str(combined_value).encode()).hexdigest()

    # create a pattern based on the seed
    img_size = 256
    img = Image.new("RGB", (img_size, img_size), "white")
    draw = ImageDraw.Draw(img)

    # use the unique pattern seed to generate a random, but deterministic pattern
    random.seed(unique_pattern_seed)

    # fill the image with some randomized shapes based on the input values
    for i in range(50):  # draw 50 random circles (change it if you want)
        x = random.randint(0, img_size)
        y = random.randint(0, img_size)
        radius = random.randint(10, 30)
        color = (random.randint(0, 255), random.randint(0, 255), random.randint(0, 255))
        draw.ellipse((x - radius, y - radius, x + radius, y + radius), outline=color, width=2)

    # add a border using the combined value as the color
    border_color = (int(unique_pattern_seed[:2], 16), int(unique_pattern_seed[2:4], 16), int(unique_pattern_seed[4:6], 16))
    draw.rectangle([0, 0, img_size-1, img_size-1], outline=border_color, width=10)

    # show the pattern
    img.show()
    img.save("your_unique_pattern.png")

    return unique_pattern_seed  # Return the pattern seed for reference


# ask for inputs
birth_date = input("Enter your birth date (YYYY-MM-DD): ")  # example: 1453-05-29
favorite_color = input("Enter your favorite color (hex, e.g. #6ed6e6): ")  # example: #6ed6e6
license_plate = input("Enter your license plate number (number, e.g. 34 (for Istanbul)): ")  # example: 34XYZ123

# generate the pattern based on the inputs
pattern_seed = generate_pattern(birth_date, favorite_color, license_plate)
print(f"Generated Pattern Seed: {pattern_seed}")
