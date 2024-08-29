# IMG-EDITOR



from PIL import Image, ImageEnhance, ImageFilter
import os

# Paths
path = r"C:\Users\antho\Downloads"
pathOut = os.path.join(path, 'editedImgs')

# Ensure the output directory exists
if not os.path.exists(pathOut):
    os.makedirs(pathOut)

# Process each image in the directory
for filename in os.listdir(path):
    try:
        # Only process files with common image extensions
        if filename.lower().endswith(('.png', '.jpg', '.jpeg', '.bmp', '.gif')):
            img = Image.open(os.path.join(path, filename))

            # Apply various image edits
            edit = img.filter(ImageFilter.SHARPEN)
            edit = edit.convert('L')
            edit = edit.rotate(-90)
            edit = edit.resize((img.width // 2, img.height // 2))  # Example: resize to half the original size
            enhancer = ImageEnhance.Contrast(edit)
            edit = enhancer.enhance(1.5)  # Enhance contrast

            # Save the edited image
            clean_name = os.path.splitext(filename)[0]
            edit.save(os.path.join(pathOut, f"{clean_name}_edited.jpg"))

            print(f"Processed {filename} successfully!")

    except Exception as e:
        print(f"Failed to process {filename}: {e}")
