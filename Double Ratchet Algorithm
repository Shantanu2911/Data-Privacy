# Double Ratchet Algorithm

## Overview
The Double Ratchet Algorithm is a cryptographic protocol designed to provide **end-to-end encryption** with strong security properties such as **forward secrecy** and **post-compromise security**. It combines two types of key ratchets:

- **Diffie-Hellman (DH) Ratchet**: For asynchronous key agreement.
- **Symmetric-key Ratchet**: For continuous key evolution with each message.

This algorithm is the backbone of secure messaging protocols used by apps like **Signal** and **WhatsApp** to protect users' messages.

---

## Key Concepts

- **Forward Secrecy**: Ensures that if current keys are compromised, past messages remain secure.
- **Post-Compromise Security**: If a key is compromised, future keys are refreshed automatically to regain security.
- **Ratchet**: A method to continuously update cryptographic keys, making it infeasible to recover past or future keys from a compromised key.

---

## Components

1. **Diffie-Hellman (DH) Ratchet**
   - Each party generates ephemeral DH key pairs.
   - When a new DH public key is received, the shared secret is updated.
   - This allows for asynchronous communication without prior coordination.

2. **Symmetric-key Ratchet**
   - A Key Derivation Function (KDF) evolves keys forward with each message.
   - Derives **message keys** from chain keys, used to encrypt/decrypt individual messages.

---

## How It Works

### Initialization
- Both parties start with a shared secret established via an initial DH key exchange.
- They maintain a **root key (RK)** and two **chain keys (CK)**: one for sending and one for receiving.

### Sending a message
- The sender uses the sending chain key to derive a new **message key (MK)** via a KDF.
- Encrypts the message with the message key.
- Optionally sends the sender’s current DH public key to initiate a DH ratchet step if necessary.

### Receiving a message
- The receiver checks if the sender’s DH public key has changed.
  - If yes, performs a DH ratchet step:
    - Runs DH key agreement using the sender's new DH public key and receiver’s private DH key.
    - Updates the root key and resets chain keys.
- Uses the receiving chain key to derive the message key.
- Decrypts the message.

### DH Ratchet Step
- Occurs when a new DH public key is received.
- Updates the **root key (RK)** via a KDF using the DH shared secret.
- Resets the sending and receiving chain keys.
- Enables forward secrecy and post-compromise security.

---

## Terminology

| Term             | Description                                |
|------------------|--------------------------------------------|
| Root Key (RK)    | Master secret, updated after DH ratchets  |
| Chain Key (CK)   | Used to derive message keys via KDF        |
| Message Key (MK) | Key derived from CK to encrypt/decrypt messages |
| DH Key Pair      | Ephemeral public/private key pairs used in DH ratchet |
| KDF              | Key Derivation Function for evolving keys  |

---

## WhatsApp and the Double Ratchet Algorithm

WhatsApp employs the Double Ratchet Algorithm as part of its **Signal Protocol** implementation to secure messages end-to-end. Here's how WhatsApp leverages the algorithm:

- **Initialization**: When users initiate a conversation, WhatsApp performs a key exchange based on the **X3DH (Extended Triple Diffie-Hellman)** protocol to establish an initial shared secret.

- **Message Encryption**: Every message sent uses the Double Ratchet to derive a fresh message key, ensuring that even if a message key is compromised, it doesn't affect other messages.

- **Handling Offline and Asynchronous Communication**: Since users are not always online simultaneously, the DH ratchet allows WhatsApp to update keys asynchronously when the recipient comes online, without needing immediate responses.

- **Group Messaging**: WhatsApp extends the Double Ratchet to support groups by maintaining separate ratchets for each member, ensuring message secrecy in group chats.

- **Security Guarantees**:
  - Forward secrecy protects past messages if current keys are compromised.
  - Post-compromise security allows WhatsApp to recover from key exposure due to automatic key updates.
  - Message keys are used only once and then discarded, preventing replay attacks.

---

## Security Properties

- **Confidentiality**: Each message is encrypted with a unique key.
- **Forward Secrecy**: Compromise of current keys does not compromise past messages.
- **Post-Compromise Security**: Automatic recovery from key exposure ensures long-term security.
- **Asynchronous Messaging**: Parties can send messages without being simultaneously online.
- **Integrity and Authenticity**: Messages are authenticated to prevent tampering.

---

## References

- [Signal Protocol - Double Ratchet Algorithm Specification](https://signal.org/docs/specifications/doubleratchet/)
- [Moxie Marlinspike’s Blog: The Double Ratchet Algorithm](https://signal.org/blog/the-double-ratchet-algorithm/)
- [WhatsApp Security Overview](https://www.whatsapp.com/security/)
- [Cryptography Engineering Blog - Explaining the Double Ratchet](https://blog.cryptographyengineering.com/2016/03/17/double-ratchet-algorithm/)

---

## Further Reading and Resources

- [Signal Protocol GitHub Repository](https://github.com/signalapp/libsignal-protocol-c)
- [Double Ratchet Algorithm - Wikipedia](https://en.wikipedia.org/wiki/Double_Ratchet_Algorithm)

---

Feel free to reach out if you want me to add diagrams or sample code snippets to this file!
