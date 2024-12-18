# StreamlinedCryptography

StreamlinedCryptography is a Python library that provides a simple and easy-to-use interface for encryption and decryption. It is built on top of the popular cryptography library and provides a high-level API for common cryptographic operations.

## Features

- Symmetric encryption and decryption (AES-GCM)
- Asymmetric encryption and decryption (Elliptic Curve SECP256R1)
- High-level abstractions for common cryptographic operations
- Strict type enforcement

## Installation

You can install StreamlinedCryptography using pip:

```bash
pip install StreamlinedCryptography
```

## Usage

Here's an example of how you can use StreamlinedCryptography to encrypt and decrypt a message:

```python
from StreamlinedCryptography import encrypt_symmetric, decrypt_symmetric, SymmetricEncryptResult

data = b"Test Message"
password = b"Password"

encrypted = encrypt_symmetric(password, data)  # Encrypted data is a SymmetricEncryptResult object
serialized = encrypted.serialize()

deserialized = SymmetricEncryptResult.from_serialized(serialized)
decrypted = decrypt_symmetric(password, deserialized)

print(decrypted.decode("utf-8"))
```

and here's an example of how you can use StreamlinedCryptography to encrypt and decrypt a message using asymmetric encryption:

```python
from StreamlinedCryptography import encrypt_symmetric, decrypt_symmetric, SymmetricEncryptResult  # Symmetric imports
from StreamlinedCryptography import derive_secret, AsymmetricPrivateKey, AsymmetricPublicKey  # Asymmetric imports

# Using ECC to derive a shared secret

data = b"Test Message"

alice_private_key = AsymmetricPrivateKey.generate()
alice_public_key = AsymmetricPublicKey.from_private_key(alice_private_key)

bob_private_key = AsymmetricPrivateKey.generate()
bob_public_key = AsymmetricPublicKey.from_private_key(bob_private_key)

alice_secret = derive_secret(alice_private_key, bob_public_key)
bob_secret = derive_secret(bob_private_key, alice_public_key)

assert alice_secret == bob_secret  # The shared secret is the same for both parties

# Using the shared secret to encrypt and decrypt data

encrypted = encrypt_symmetric(alice_secret, data)  # Encrypted data is a SymmetricEncryptResult object

decrypted = decrypt_symmetric(bob_secret, encrypted)

print(decrypted.decode("utf-8"))
```

## License

StreamlinedCryptography is licensed under the MIT license. See the [LICENSE](LICENSE) file for more information.

## Requirements

StreamlinedCryptography was built and tested on Python 3.12, I am unsure if it will work on earlier versions of Python.  
StreamlinedCryptography requires the [cryptography](https://pypi.org/project/cryptography/) library.

## Acknowledgements

StreamlinedCryptography is built on top of the [cryptography](https://pypi.org/project/cryptography/) library. We would like to thank the authors and contributors of the cryptography library for their hard work and dedication.
