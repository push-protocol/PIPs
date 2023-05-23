# About Verification - Definitions / Specs

## What is Verification?

Push Chat incorporates a rigorous verification process divided into User Verification and Chat Verification. User Verification ensures the authenticity of user data during creation or modification, while Chat Verification is responsible for validating the messages exchanged within the chat system. This dual-layered verification mechanism serves to uphold the integrity of both users and their communication, fortifying the overall security of our system.

## Specifications

In Push Chat, we place a strong emphasis on the verification process to ensure data integrity and user authenticity. To achieve this, we implement two levels of verification: User Verification and Chat Verification.

### User Verification

User verification is primarily conducted when there's any creation or modification of user data. This includes details such as the user's name, chosen encryption type (which determines how the PGP private key is encrypted), and an encrypted password (particularly relevant for NFT chat).

This verification process is designed to ensure the integrity and authenticity of the user information being created or modified. When such changes occur, the system automatically triggers the verification process to validate the authenticity of the user and the legitimacy of the changes being made. It's an integral step in maintaining the security of the user accounts and in turn, the overall integrity of our chat system.

### Chat Verification

On the other hand, chat verification is the validation of the messages exchanged within the chat system. Every time a message is sent or received, the system and the client both execute a verification process.

This process involves verifying the signature attached to each message. As each message is signed with the sender's private key, the system and the client can use the sender's public key to verify the signature, thus confirming the authenticity and integrity of the message. Both Push Nodes and client applications participate in this verification process.

By utilizing the Push Nodes for this verification, we ensure a layer of server-side security. Additionally, client-side verification adds an extra layer of security, verifying the message upon receipt, ensuring its integrity hasn't been compromised during transmission.

Through these two verification processes, our chat system aims to provide a secure environment for users to communicate, ensuring the authenticity of users and the integrity of the messages being exchanged.
