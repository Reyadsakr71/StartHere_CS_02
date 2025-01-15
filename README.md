# StartHere_CS_02
PIXEL MANIPULATION FOR IMAGE ENCRYPTION.py

from PIL import Image
import numpy as np


# Function to encrypt the image
def encrypt_image(image_path, key):
    # Open the image and convert it to RGB (if not already in RGB format)
    img = Image.open(image_path)
    img = img.convert("RGB")

    # Convert the image to a numpy array to manipulate pixel values
    img_array = np.array(img)

    # Apply encryption: XOR the pixel values with the key
    encrypted_array = img_array ^ key

    # Convert the encrypted numpy array back to an image
    encrypted_image = Image.fromarray(encrypted_array)
    encrypted_image.save("encrypted_image.png")
    encrypted_image.show()

    print("Image encrypted and saved as 'encrypted_image.png'")


# Function to decrypt the image
def decrypt_image(encrypted_image_path, key):
    # Open the encrypted image
    encrypted_img = Image.open(encrypted_image_path)
    encrypted_img = encrypted_img.convert("RGB")

    # Convert the encrypted image to a numpy array
    encrypted_array = np.array(encrypted_img)

    # Apply decryption: XOR the encrypted pixel values with the key (same operation as encryption)
    decrypted_array = encrypted_array ^ key

    # Convert the decrypted numpy array back to an image
    decrypted_image = Image.fromarray(decrypted_array)
    decrypted_image.save("decrypted_image.png")
    decrypted_image.show()

    print("Image decrypted and saved as 'decrypted_image.png'")


# Main function to get user input and perform encryption or decryption
def main():
    # User input for image path and encryption key
    image_path = input("Enter the path to the image: ")
    key = int(input("Enter a numeric key for encryption (e.g., 123): "))
    # Encrypt the image
    encrypt_image(image_path, key)
    # Ask user if they want to decrypt the image
    decrypt_choice = input("Do you want to decrypt the image? (yes/no): ")
    if decrypt_choice.lower() == 'yes':
        decrypt_image("encrypted_image.png", key)


# Run the main function
if __name__ == "__main__":
    main()
