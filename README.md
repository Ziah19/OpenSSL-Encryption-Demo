# OpenSSL Encryption Demo
> Text encryption and decryption using AES-256, DES-CBC and RSA-2048 via OpenSSL on Kali Linux.



## Environment
| Item | Detail |
|------|--------|
| OS | Kali Linux (VMware) |
| Tool | OpenSSL |
| Interface | Command-line |



## What is AES-256-CBC?

**AES (Advanced Encryption Standard)** is a symmetric encryption algorithm, one key encrypts and the same key decrypts. It is the global standard for data encryption, used in banking, government systems, and secure communications.

- **256** → key size in bits. Larger = stronger. 2²⁵⁶ possible keys makes brute-force attacks impossible with current technology.
- **CBC (Cipher Block Chaining)** → each block of data is mixed with the previous encrypted block before being encrypted. This means identical words in your plaintext won't produce identical patterns in the ciphertext.
- **Salt** → random data added before encryption so the same password never produces the same output twice.
- **PBKDF2** → converts your plain password into a cryptographically strong key before it's used.



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



## Results

| Action | Outcome |
|--------|---------|
| Encrypt message.txt | Produced unreadable ciphertext in message_aes.enc |
| Decrypt with correct password | Original message restored perfectly |
| Decrypt with wrong password | Failed, encryption integrity confirmed |


---

## DES-CBC Encryption

**DES (Data Encryption Standard)** is a symmetric encryption algorithm — same concept as AES, one key encrypts and decrypts. It was the global standard before AES but was cracked in under 24 hours in 1999 due to its weak 56-bit key. It is included here for educational comparison only.



## DES Commands

### Encrypt
```bash
openssl enc -des-cbc -salt -pbkdf2 -in message.txt -out message_des.enc
```

### Decrypt
```bash
openssl enc -des-cbc -pbkdf2 -d -in message_des.enc -out message_des_decrypted.txt
```



## AES vs DES

| | AES-256 | DES |
|--|---------|-----|
| Key size | 256-bit | 56-bit |
| Status | Industry standard | Broken / legacy |
| Crackable? | No | Yes, cracked in 1999 |
| Used today? | Yes | No, educational only |
---


## RSA Encryption

**RSA (Rivest–Shamir–Adleman)** is an asymmetric encryption algorithm, it uses two mathematically linked keys. The public key encrypts, the private key decrypts. It is the foundation of HTTPS, SSH, and email encryption.

- **2048-bit key** → minimum recommended size for RSA today
- **Public key** → share freely. Anyone can use it to encrypt a message for you
- **Private key** → never share. Only you can use it to decrypt messages
- **.pem format** → the file format RSA keys are stored in

---

## RSA Commands

### Generate Private Key
```bash
openssl genrsa -out private.pem 2048
```

### Extract Public Key
```bash
openssl rsa -in private.pem -pubout -out public.pem
```

### Encrypt
```bash
openssl pkeyutl -encrypt -inkey public.pem -pubin -in message.txt -out message_rsa.enc
```

### Decrypt
```bash
openssl pkeyutl -decrypt -inkey private.pem -in message_rsa.enc -out message_rsa_decrypted.txt
```

---

## AES vs DES vs RSA

| | AES-256 | DES | RSA-2048 |
|--|---------|-----|----------|
| Type | Symmetric | Symmetric | Asymmetric |
| Keys | 1 shared key | 1 shared key | Public + Private |
| Key size | 256-bit | 56-bit | 2048-bit |
| Speed | Fast | Fast | Slow |
| Status | Industry standard | Broken / legacy | Industry standard |
| Best used for | Encrypting large data | Education only | Key exchange, signatures |

---

## Project Files



## Project Files
1. Aes encryption demo.png
2. des encryption.png
3. rsa_1
4. rsa_2
