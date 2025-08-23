# Data-Privacy
Data Privacy (DSE – Sem V) explores principles of protecting sensitive data, privacy laws, cryptographic methods, anonymization, and ethical issues in data use—equipping students to understand breaches and ensure responsible data handling.
# 🔐 Simple Guide to Cryptography & Privacy


## Table of contents
- [About this repo](#about-this-repo)  
- [Quick links](#quick-links)  
- [Core ideas & basics](#core-ideas--basics)  
- [Crypto building blocks & protocols](#crypto-building-blocks--protocols)  
- [Network security & PETs](#network-security--privacy-enhancing-technologies-pets)  
- [Advanced crypto protocols](#advanced-crypto-protocols)  
- [Practical stuff & tools](#practical-stuff--tools)  
- [Threats & attacks](#threats--attacks)  
- [What’s coming next (emerging)](#whats-coming-next-emerging)  
- [References & further reading](#references--further-reading)  
---

## About this repo
This is a compact, hands-on-ish summary of crypto and privacy topics I’m learning. I wrote it for other beginners — short explanations, links to more detailed stuff, and a few ideas to try. It’s not perfect and I probably messed up some terms, so please correct me if you find errors.

---

## Quick links
(Handy links I used / recommend)
- Verifiable Credentials (W3C): https://www.w3.org/TR/verifiable-claims/  
- GDPR intro: https://gdpr.eu/  
- TLS / RFCs: https://www.rfc-editor.org/  
- NIST Post-Quantum project: https://csrc.nist.gov/projects/post-quantum-cryptography  
- Microsoft SEAL (homomorphic): https://github.com/microsoft/SEAL  
- ZoKrates (ZK tooling): https://github.com/Zokrates/ZoKrates  
- OpenSSL: https://www.openssl.org/  
- libsodium: https://libsodium.org/  
- zkproof intro: https://zkproof.org/  
- IACR ePrint archive: https://eprint.iacr.org/

---

## Core ideas & basics
(Short, plain words about the main concepts.)

### Identity & credentials
- People prove who they are using: **something they know** (password), **something they have** (token), **something they are** (biometrics).  
- Fancy newer things: **Verifiable Credentials** and **Self-Sovereign Identity** — they let a person keep and share claims about themselves without a central database.

### Digital signatures
- Used to prove who sent a message and that it wasn’t changed. Examples: `ECDSA`, `EdDSA`.  
- Good for authenticity, but signatures can sometimes be linked across systems (privacy risk).

### PKI & certificates
- Public Key Infrastructure (X.509 certificates) is what browsers use to trust websites (TLS). The downside: it relies on Certificate Authorities (CAs), and if they get compromised it’s bad.

### Confidentiality vs anonymity
- **Confidentiality** = keep the content secret (e.g., TLS, AES).  
- **Anonymity** = hide who is communicating (e.g., Tor). Both are important but different.

---

## Crypto building blocks & protocols
(Basics of the cryptography tools people actually use.)

### Encryption
- **Symmetric** (same key): AES, ChaCha20. Fast for big data.  
- **Asymmetric** (public/private): RSA, ECC. Good for key exchange and signatures.  
- **Hybrid**: Use asymmetric to share a symmetric key, then use symmetric for the data (this is what TLS does).

### Hashes & MACs
- Hashes (SHA-2/3, BLAKE2) turn data into fixed-size digests. Use salted password hashes (Argon2, bcrypt).  
- MACs (HMAC) verify data integrity + authenticity when you share a secret key.

### Key exchange & forward secrecy
- Diffie–Hellman / ECDH lets two parties agree on a key without sending it directly. Ephemeral versions (ECDHE) give **forward secrecy**.

### Signatures
- Options: RSA-PSS, ECDSA, Ed25519. Ed25519 is modern and easier to use correctly.

---

## Network security & privacy-enhancing technologies (PETs)
(How to hide or protect data on the wire and hide metadata.)

### TLS / HTTPS
- Use TLS 1.3 where possible. It makes a secure channel between client and server. Learn the basics: how certs, key exchange, and ciphers work.

### VPNs
- VPNs (WireGuard, OpenVPN) tunnel traffic and hide your IP from local observers. They don’t make you anonymous on the internet by default (the VPN provider sees traffic).

### Tor & mixnets
- Tor uses onion routing to hide endpoints. Mixnets add delays/batching to hide patterns better (but are slower).

---

## Advanced crypto protocols
(Some cooler/smarter stuff — not simple, but useful.)

### Zero-knowledge proofs (ZKP)
- Prove you know something without revealing it. Useful for privacy-preserving authentication, blockchains, etc. Types: zk-SNARKs, zk-STARKs.

### Secure Multi-Party Computation (SMPC)
- Multiple parties compute a function together without revealing their private inputs. Good for private analytics.

### Homomorphic encryption (HE)
- Do computations on encrypted data (slow but useful in special cases). Libraries: Microsoft SEAL, HElib.

### Secret sharing & threshold crypto
- Split a secret into shares (Shamir) so no single person has it. Useful for backups and distributed signing.

---

## Practical stuff & tools
(Some libraries and tips I use / recommend trying)

### Language libraries
- Python: `cryptography`, `PyNaCl`  
- JS: builtin `crypto`, `libsodium.js`  
- C/C++: OpenSSL, libsodium  
- HE & ZK tooling: Microsoft SEAL, ZoKrates

### Tips for implementing crypto
- Use well-tested libraries (don’t invent your own crypto).  
- Prefer AEAD ciphers (like `AES-GCM`) to get encryption + integrity.  
- Use Argon2 or bcrypt for password hashing with a salt.  
- Don’t log secrets. Rotate keys if leaked. Use secure RNGs.

---

## Threats & attacks
(Be aware — attacks are not always the fancy math ones.)

### Side-channel attacks
- Timing, power, or cache side-channels can leak keys. Constant-time code helps.

### Traffic analysis
- Even if traffic is encrypted, packet sizes and timing can leak info. Padding and batching can help.

### Crypto failures & misconfigurations
- Using old algorithms (MD5, SHA-1), bad randomness, reusing keys — these lead to breaks. Keep standards and params up-to-date.

### Social engineering & ops mistakes
- Phishing, weak passwords, leaked S3 buckets, and bad configs are still the most common causes of breaches.

---

## What’s coming next (emerging)
(Short notes about future/active research areas.)

- **Post-quantum crypto (PQC)**: new algorithms that should resist quantum attacks (see NIST PQC).  
- **Privacy on blockchains**: zk proofs, confidential transactions, mixers.  
- **AI & privacy**: differential privacy, federated learning, encrypted inference.

---

## References & further reading
(Stuff I used while writing this and links you can read next.)

- Books: *Applied Cryptography* (Schneier), *Serious Cryptography* (Aumasson)  
- NIST PQC: https://csrc.nist.gov/projects/post-quantum-cryptography  
- ZoKrates: https://github.com/Zokrates/ZoKrates  
- Microsoft SEAL: https://github.com/microsoft/SEAL  
- OpenSSL: https://www.openssl.org/  
- libsodium: https://libsodium.org/  
- zkproof: https://zkproof.org/  
- IACR ePrint: https://eprint.iacr.org/

---

