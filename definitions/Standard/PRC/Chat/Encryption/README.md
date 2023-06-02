# About Encryption - Definition / Specs

## What is Chat Encryption?

On this section we describe all the encryption algorithms and processes used to secure the chat messages.

## Specifications

This document outlines the first version of our chat messaging system's encryption process. We employ a double encryption methodology, leveraging the Advanced Encryption Standard (AES) for encrypting the message content and Pretty Good Privacy (PGP) for securing the AES key itself. This approach guarantees message confidentiality and integrity, ensuring that only the intended recipients can decipher the original message. The subsequent sections will provide detailed explanations of our encryption and decryption mechanisms, emphasizing the robust security measures we've implemented to protect your communications.

Here below are the encryption types (versions) that we currently support:

| encryption type | Description                                              |
| --------------- | -------------------------------------------------------- |
| `pgp`           | Double encryption schema that leverages both AES and PGP |

## Encryption type: `pgp`

### Message Encryption Process

1. Generate a Random AES Key: For each message, a random AES key is generated. This is a symmetric key that will be used to encrypt the actual message content.

2. Encrypt the Message Payload: The generated AES key is then used to encrypt the message payload. The output of this process is a ciphertext - a scrambled version of your message that can only be decrypted using the same AES key.

3. Encrypt the AES Key: This is where asymmetric encryption comes into play. We take the AES key and encrypt it using the PGP private keys of all users involved in the conversation. This means that only the users who hold the corresponding PGP public keys can decrypt this AES key.

4. Add Encrypted AES Key to Payload: The encrypted AES key is then added to the message payload.

### Message Decryption Process

1. Retrieve PGP Public Key: When a user receives a message, they first retrieve their PGP public key from the server.

2. Decrypt the AES Key: The user then uses their PGP public key to decrypt the encrypted AES key that was sent along with the message payload.

3. Decrypt the Message Content: Once the AES key has been decrypted, it is then used to decrypt the message content. What they get is the original plaintext message that was sent.
