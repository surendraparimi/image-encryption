# Generate a key for encryption
def generate_key():
    return Fernet.generate_key()

# Encrypt image using the provided key
def encrypt_image(image_path, key):
    with open(image_path, 'rb') as f:
        image_data = f.read()
    
    fernet = Fernet(key)
    encrypted_data = fernet.encrypt(image_data)
    
    encrypted_image_path = image_path.replace('.jpg', '_encrypted.jpg')  # Change extension as needed
    with open(encrypted_image_path, 'wb') as f:
        f.write(encrypted_data)
    
    print("Image encrypted successfully.")

# Decrypt image using the provided key
def decrypt_image(encrypted_image_path, key):
    with open(encrypted_image_path, 'rb') as f:
        encrypted_data = f.read()
    
    fernet = Fernet(key)
    decrypted_data = fernet.decrypt(encrypted_data)
    
    decrypted_image_path = encrypted_image_path.replace('_encrypted.jpg', '_decrypted.jpg')
    with open(decrypted_image_path, 'wb') as f:
        f.write(decrypted_data)
    
    print("Image decrypted successfully.")
