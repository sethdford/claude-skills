---
name: cryptography-selection
description: Select appropriate cryptographic algorithms and parameters for encryption, hashing, key derivation, and digital signatures.
---

# Cryptography Selection

Choose appropriate cryptographic algorithms and parameters for your security requirements.

## Context

You are a senior security architect selecting cryptography for $ARGUMENTS. Cryptography is critical but easy to misuse; wrong algorithm, weak parameters, or misapplication can render it useless.

## Domain Context

- **Symmetric Encryption** (shared key): AES-256-GCM for data at rest and in transit
- **Asymmetric Encryption** (public key): Only for key exchange, not bulk data (too slow); prefer Elliptic Curve Diffie-Hellman (ECDH)
- **Hashing**: SHA-256 or SHA-3 for integrity; Argon2 for passwords
- **Digital Signatures**: RSA (2048+ bits) or ECDSA (P-256+) for authentication
- **Key Derivation**: Argon2 for passwords, HKDF for key derivation from shared secret

## Instructions

1. **Encryption in Transit**:
   - Use **TLS 1.2+** (never SSL 3.0, TLS 1.0, TLS 1.1)
   - Cipher suites: Modern (ChaCha20-Poly1305, AES-128-GCM) with forward secrecy (ECDHE, DHE)
   - Disable NULL, EXPORT, DES, RC4, and anonymous cipher suites
   - Require HTTPS everywhere; use HSTS header

2. **Encryption at Rest**:
   - **AES-256-GCM** (preferred; provides authentication + encryption)
   - Or **ChaCha20-Poly1305** (good alternative, faster on CPUs without AES-NI)
   - Never use AES-ECB, AES-CBC without authentication, or RC4
   - Unique IV/nonce for each encryption (GCM mode requires this; misuse = complete compromise)

3. **Key Management**:
   - **Never hardcode keys** in code; load from environment or secure vault
   - **Rotate keys** annually or after suspected compromise
   - Use **key derivation function** (HKDF, PBKDF2) to derive keys from shared secret
   - **Separate keys** per purpose (encryption key ≠ signing key ≠ API key)

4. **Password Hashing**:
   - **Argon2id** (time=2 iterations, 19 MiB memory, parallelism=1)
   - Or **bcrypt** (cost=12+) or **PBKDF2** (100,000+ iterations)
   - Never MD5, SHA1, or unsalted SHA256; too fast, can be brute-forced
   - Salt: Use unique, random salt per password (standard in bcrypt, Argon2)

5. **Digital Signatures**:
   - RSA: 2048-bit minimum (4096 for long-term keys, legacy compatibility)
   - ECDSA: P-256 (NIST) or Curve25519; modern, shorter keys
   - Never MD5 or SHA1 for signing; use SHA-256 or SHA-3
   - Key management: Private key in secure vault, public key distributed widely

6. **Hash Functions**:
   - **SHA-256** or **SHA-3** for integrity checking, digital signatures
   - Never MD5 or SHA1; collision vulnerabilities known (SHA1 collision published 2017)
   - HMAC (Hash-based Message Authentication Code): Use for message authentication with secret key

## Anti-Patterns

- Using crypto libraries but implementing custom logic (e.g., custom padding, custom mode); **use standard library functions without modification**
- Reusing IVs/nonces in GCM mode; **catastrophic: attacker can recover plaintext and forge messages**
- Hard-coding keys; **always use key management systems (AWS KMS, HashiCorp Vault, Azure Key Vault)**
- Encrypting without authentication (AES-CBC); **unauthenticated encryption allows padding oracle and bit-flipping attacks**
- Storing keys in the database alongside encrypted data; **keys should be managed separately, in a vault**
- Using `openssl enc` or similar simple CLI tools for production; **they lack authenticated encryption by default**

## Further Reading

- NIST SP 800-175B (Guideline for Using Cryptographic Standards): https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-175B.pdf
- OWASP Cryptographic Storage Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Cryptographic_Storage_Cheat_Sheet.html
- Crypto101 (free book): https://www.crypto101.io/
- Serious Cryptography (Aumasson, 2018): Practical guidance on cryptography
