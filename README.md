# AddClassLabelsNorthernLights

import os
import re

class_names = ['anthroprogenic', 'artificial_light', 'aurora', 'clouds', 'long_exposure', 'moon']
class_numbers = [0, 1, 2, 3, 4, 5]  # Class names

# Define the directory you want to traverse
root_dir = r'X:\Aurora\MainFileAurora\AuroraSorted_PWN\used_images'

# Define a regular expression pattern to match numbers
number_pattern = re.compile(r'\d+')

# Walk through the directory tree
for root, dirs, files in os.walk(root_dir):
    print(f'Currently in directory: {root}')

    short_root = root.replace(root_dir, '')

    # go through all files in the current directory
    for file in files:
        matching_strings = []
        for s in class_names:
            if s in short_root:
                matching_strings.append(s)

        print({file})
        print(matching_strings)
        print(short_root)
        print(root)

        # Check if the file is a photo file (you may need to adjust the condition based on your file types)
        if file.endswith('.jpg') or file.endswith('.png'):
            # Read the content of the photo file in binary mode
            with open(os.path.join(root, file), 'rb') as f:
                content = f.read()

            # Find all numbers in the content using the regular expression pattern
            numbers = number_pattern.findall(str(content))

            # Write the output to a text file
            output_filename = f'{file}_output.txt'
            with open(output_filename, 'w', encoding='utf-8') as output_file:
                if numbers:
                    output_file.write(f"Numbers found in {file}: {numbers}\n")
                else:
                    output_file.write(f"No numbers found in {file}\n")

            print(f"Output saved to {output_filename}")
