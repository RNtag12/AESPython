<h1>Files AES Encryption and Decryption with Python</h1>
This project explains how to utilize a Python-based code for encrypting and decrypting files and directories. The script employs advanced cryptographic technique (AES) to ensure the security and integrity of your data.

## General Information
Cryptography is a cornerstone of cybersecurity, providing the tools necessary to keep sensitive information secure. The cryptography library in Python is a powerful resource for implementing secure encryption and decryption methods. This utility harnesses the cryptography library to create a secure method for encrypting and decrypting files using a password-derived key. This ensures that only those with the correct password can access the contents of the files, providing an extra layer of security.

<h2> Project Description</h2>
The File AES Encryption and Decryption Program is a Python-based application that encrypts and decrypts files using the Advanced Encryption Standard (AES) algorithm. The PBKDF2HMAC key derivation function is used to generate a secure key from a user-provided password, ensuring that the encrypted files can only be decrypted with the same password. This utility is capable of processing both individual files and entire directories, using threading to handle multiple files concurrently to enhance efficiency. Additionally, Fernet symmetric encryption is used, guaranteeing that the data remains confidential and untampered.
<br />

## Features
- Password-based key generation using PBKDF2HMAC
- Encryption and decryption of individual files
- Support for directory encryption and decryption
- Threading for concurrent file processing
- Secure key storage using salt

<h2>Libraries and modules </h2>

- <b>os, base 64</b> 
- <b>pyfiglet</b>
- <b>hashes</b> 
- <b>time</b>
- <b>threading </b>
- <b>Termcolor</b>

<h2>IDE </h2>
<b>Jupiter Notebook </b> 

## How It Works
- <b> Key Generation</b>
The utility converts a user-provided password into a secure key using the PBKDF2HMAC key derivation function. This function includes a randomly generated salt to enhance security.

```python
def password(passwd):
    password = passwd.encode()  # Convert the password string to bytes using UTF-8 encoding
    salt = os.urandom(16)  # Generate a random salt
    kdf = PBKDF2HMAC(
        algorithm=hashes.SHA256(),
        length=32,
        salt=salt,
        iterations=100000,
        backend=default_backend()
    )
    k = base64.urlsafe_b64encode(kdf.derive(password))
    return k
```

- <b> Encryption Function</b>
The encrypt function reads the contents of a file, encrypts it using the derived key, and writes the encrypted data to a new file with a .en extension. The original file is then deleted.
```python
def encrypt(key, file):
    try:
        with open(file, "rb") as fname:
            data = fname.read()
        
        # Extract file name and extension
        fl, ext = os.path.splitext(file)
        
        # Create a Fernet key from the provided key
        fkey = f(key)
        
        # Encrypt the file data using Fernet
        enc = fkey.encrypt(data)
        
        # Write the encrypted data to a new file with a .en extension
        with open(str(fl[0:]) + ext + '.en', 'wb') as encfile:
            encfile.write(enc)
        
        # Remove the original unencrypted file
        os.remove(file)
        
        # Print the results
        print("                      ")
        print(f"File encrypted successfully ")
        print("                               ") 
        print(f"{file} ==> {str(fl[0:]) + ext + '.en'}")
    
    except Exception as e:
        print("                      ")
        print("Something went wrong", e)
```

- <b> Decryption Function</b>
The decrypt function reads the encrypted file, extracts the salt, derives the key using the password and salt, decrypts the data, and writes the original content back to a file.
```python
def decrypt(key, file):
    try:
        with open(file, "rb") as fname:
            data = fname.read()
        
        # Create a Fernet key from the provided key
        fkey = f(key)
        
        # Extract file name and extension
        fl, ext = os.path.splitext(file)
        
        # Decrypt data using Fernet
        dec = fkey.decrypt(data)
        
        # Write the decrypted data to a new file with the original file name
        with open(str(fl[0:]), 'wb') as decfile:
            decfile.write(dec)
        
        # Remove the original encrypted file
        os.remove(file)
        print("                      ")
        print(f"File decrypted successfully")
        print("                             ")
        print(f"{file} ==> {fl[0:]}")
    
    except:
        print("                      ")
        print("Something went wrong")
```

## Steps to Execute the Project
- Clone the repository or download the script.
- Install the required dependencies and run the code:
```python
pip install cryptography pyfiglet termcolor
```
- Follow the prompts to encrypt or decrypt files or directories.

## Conclusion
This project  offers a robust and user-friendly method for securing files using password-based encryption. By leveraging the cryptography library and implementing best practices for key derivation and file handling, this project ensures that sensitive data remains protected from unauthorized access.

