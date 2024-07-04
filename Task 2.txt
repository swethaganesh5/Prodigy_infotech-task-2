from PIL import Image
import numpy as np
import tkinter as tk
from tkinter import filedialog

# Load the image
def load_image(image_path):
    return Image.open(image_path)

# Encrypt the image
def encrypt_image(image_array, key=42):
    encrypted_array = (image_array.astype(np.uint16) + key) % 256
    return encrypted_array.astype(np.uint8)

# Decrypt the image
def decrypt_image(encrypted_array, key=42):
    decrypted_array = (encrypted_array.astype(np.uint16) - key) % 256
    return decrypted_array.astype(np.uint8)

# Convert numpy array back to image
def array_to_image(array):
    return Image.fromarray(array)

# Function to open file dialog and display image
def open_file():
    file_path = filedialog.askopenfilename()
    if file_path:
        image = load_image(file_path)
        image.show()

# Function to encrypt the image and display it
def encrypt():
    file_path = filedialog.askopenfilename()
    if file_path:
        image = load_image(file_path)
        image_array = np.array(image)
        encrypted_array = encrypt_image(image_array)
        encrypted_image = array_to_image(encrypted_array)
        encrypted_image.show()

# Function to decrypt the image and display it
def decrypt():
    file_path = filedialog.askopenfilename()
    if file_path:
        image = load_image(file_path)
        image_array = np.array(image)
        decrypted_array = decrypt_image(image_array)
        decrypted_image = array_to_image(decrypted_array)
        decrypted_image.show()

# Create the GUI
root = tk.Tk()
root.title('Image Encryption Tool')

open_button = tk.Button(root, text='Open Image', command=open_file)
encrypt_button = tk.Button(root, text='Encrypt Image', command=encrypt)
decrypt_button = tk.Button(root, text='Decrypt Image', command=decrypt)

open_button.pack()
encrypt_button.pack()
decrypt_button.pack()

root.mainloop()
