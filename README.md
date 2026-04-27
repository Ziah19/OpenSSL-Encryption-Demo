# OpenSSL Encryption Demo
> Text encryption and decryption using AES-256 via OpenSSL on Kali Linux.

---

## Environment
| Item | Detail |
|------|--------|
| OS | Kali Linux (VMware) |
| Tool | OpenSSL |
| Interface | Command-line |

---

## What is AES-256-CBC?

**AES (Advanced Encryption Standard)** is a symmetric encryption algorithm, one key encrypts and the same key decrypts. It is the global standard for data encryption, used in banking, government systems, and secure communications.

- **256** → key size in bits. Larger = stronger. 2²⁵⁶ possible keys makes brute-force attacks impossible with current technology.
- **CBC (Cipher Block Chaining)** → each block of data is mixed with the previous encrypted block before being encrypted. This means identical words in your plaintext won't produce identical patterns in the ciphertext.
- **Salt** → random data added before encryption so the same password never produces the same output twice.
- **PBKDF2** → converts your plain password into a cryptographically strong key before it's used.

---

## Commands

### Encrypt
```bash
openssl enc -aes-256-cbc -salt -pbkdf2 -in message.txt -out message_aes.enc
```

### Decrypt
```bash
openssl enc -aes-256-cbc -pbkdf2 -d -in message_aes.enc -out message_aes_decrypted.txt
```

### Flag Reference
| Flag | Purpose |
|------|---------|
| `enc` | Encryption/decryption mode |
| `-aes-256-cbc` | Algorithm: AES, 256-bit key, CBC mode |
| `-salt` | Adds randomness to the encryption |
| `-pbkdf2` | Derives a secure key from the password |
| `-d` | Decrypt (remove this flag to encrypt) |
| `-in` | Input file |
| `-out` | Output file |

---

## Results

| Action | Outcome |
|--------|---------|
| Encrypt message.txt | Produced unreadable ciphertext in message_aes.enc |
| Decrypt with correct password | Original message restored perfectly |
| Decrypt with wrong password | Failed, encryption integrity confirmed |

---

## Project Files
1. Aes encryption demo.png
