# About Chat Payload - Definitions / Specs

## What is Chat Payload?

This section outlines the specifications for the chat payload in Push Chat. Messages are a JSON object that serves as the blueprint for every message sent and received in our system.

This current version of the chat payload includes a diverse range of properties, from user identifiers and message content to encryption details and timestamps. This structure is designed to be extensible, allowing for the incorporation of additional properties in future versions to suit emerging needs.

## Specifications

```typescript
export interface Message {
  fromCAIP10: string
  toCAIP10: string
  fromDID: string
  toDID: string
  messageType: string
  messageContent: string
  signature: string
  sigType: string
  timestamp?: number
  encType: string
  encryptedSecret: string
  link: string | null
}
```

| Property          | Description                                  |
| ----------------- | -------------------------------------------- |
| `fromCAIP10`      | address from where message was sent          |
| `toCAIP10`        | address to where message was sent            |
| `fromDID`         | DID from where message was sent              |
| `toDID`           | DID to where message was sent                |
| `messageType`     | type of message                              |
| `messageContent`  | content of message                           |
| `signature`       | signature of message                         |
| `sigType`         | signature type                               |
| `timestamp`       | timestamp of message                         |
| `encType`         | encryption type                              |
| `encryptedSecret` | encrypted AES secret                         |
| `link`            | link to previous message on this linked list |

### Examples

Here below is an example of a message:

```json
{
  "fromCAIP10": "eip155:0x98821462cB7Aa6fca72c6590D04bEA098c4483D0",
  "toCAIP10": "eip155:0xd9c1CCAcD4B8a745e191b62BA3fcaD87229CB26d",
  "fromDID": "eip155:0x98821462cB7Aa6fca72c6590D04bEA098c4483D0",
  "toDID": "eip155:0xd9c1CCAcD4B8a745e191b62BA3fcaD87229CB26d",
  "messageContent": "U2FsdGVkX1/QZM2yDFmx783OK3lQP5QARUBlAeeTGaU=",
  "messageType": "Text",
  "signature": "-----BEGIN PGP SIGNATURE-----\n\nwsBzBAEBCAAnBYJkYgPZCZBQPfS2j6Sx+xYhBDE96UHaT4+RRqqEklA99LaP\npLH7AACVDgf/RQdGa4wNAxaNd8rWufD3yG3E7O8Xc7siSmbvMlgFDYNB7XuA\nq/LnhUbaIIacmBTCftDi1Q1XWdXbOjb5I8wx8k/gsZjqDAt/WL1zZj/GYi6E\nNZq9pk7hcbBTX6DfqhrsACGJspIrywz0hYGKMMnY5unGbFrm0tS38YkuHUmd\nFeR9ovjq8R9kbD+XqkgpgMFo0nFalWXoj5U2hbMA6gaa/oMTsUmNGTrCDPDD\nuMkocPC1UHP9KpBg9ZCQFL81SLN9v4AmAvSsPc/n9zKzFIHgY/uYgSrx5VQA\ni8LeMPTS9A49mI4jY1ksoHqHNS1FXRPfEgMq/jWQXJtm1pzhfo4VQA==\n=AXqq\n-----END PGP SIGNATURE-----\n",
  "timestamp": 1684145115101,
  "sigType": "pgp",
  "encType": "pgp",
  "encryptedSecret": "-----BEGIN PGP MESSAGE-----\n\nwcBMA4mIJ0ko6s8yAQf/f+XZEY13wPrWyjulvE65tt2qws98qfc1h4E5531r\nvBilZBK5bwIlucH4pcRVi+6IlFPN561ycAu6D/FwZS6tubDqD2qbo6ZlZU1S\nOA7qn2WEZp0LBvGeEzQR4ySltn9a3Z0wrunIReOARLyXCI7lQJsJOp4PmePv\no5/ygSrCxTCdf6gVZwfBuDZQMlGW0LoGImnzRkdvx/zGh/zo1H5x/WwVR/hK\nXPyi9jRaC64mD7QWYAboHsFEl1P5LusEz6gzQtSDxzHbXh3FwM1xbUoZ9aGJ\nb82ADySCIlZgQlsiI0YIai4xbKYmp5LddxDIqIWY4CT6jWUIfYSbTK17+5cf\nCcHATANHghddxYDNPAEIAIDUT1RwJkfQgqchNqj65jzt1XOu1MaQhlM8hEDm\nilspf4OMGRMjApu8ihe/xVHYt10UNUOz6gLeU5VlGWgoqHLCkAvHMVGnMoJb\nOmlOIV16A5U1q2uha0vmJDLIYk7ESNn3xF5G/7TsjFLWNlEHK/f4EVsu8bWh\nlVACUmStm3IS96KCuqzFMqMcgfASUONLHHgoYZ7P1Y365gLZrnQB2OMyh0yM\na7JbfGEDjxXqlKyYC8ESzGCirO4esLzX904Zrj1+3cTC9f8QM8Qkd+bWliII\nwZtkSvU5NCDH5SPYGq4ycnkufU9Nk2f7bdWy7xh6H1kdR4QgSeMEXAupv3c2\nOGTSQAHA75mcgbyJuncFI6mtcYt7lkp6IWwYq5Tjph7a9csImcETJwwTjQeU\nmuE+9vAPCCnuZg9GktXmWZRA2tzHRyo=\n=VoM8\n-----END PGP MESSAGE-----\n",
  "link": "bafyreibvcco53h7aptxipmt7gzi5x73cw4upceto7vt2vgire2puqoeoku"
}
```

## Linked list

In Push Chat, we've implemented a linked list data structure to maintain the order and integrity of the messages within each chat. In a linked list, each element points to its preceding element, thereby creating a chain of connected elements. In the context of our system, each message contains a reference to the previous message in the conversation.

This connection is facilitated by the `link` property within our Message. The `link` property holds the unique identifier of the immediately preceding message. This ensures that each message is intrinsically linked to its predecessor, creating a seamless thread of conversation that can be easily navigated and traced back.

When initiating a new conversation, the `link` property for the very first message is set to null, indicating that there's no previous message in the conversation thread. This property is then updated with the identifier of each subsequent message, ensuring the chain of connectivity is maintained. This linked list structure not only maintains the order of the messages, but also adds an additional layer of security and integrity to the chat system.

## Storage

In Push Chat, we've adopted a robust and distributed storage strategy for messages to ensure high availability and redundancy. Each message is stored on Push Nodes, which are servers optimized for real-time message delivery and notifications. These nodes provide a fast and efficient means of accessing and delivering the chat messages in real time.

To further enhance data durability and accessibility, we also replicate each message on the InterPlanetary File System (IPFS). IPFS is a peer-to-peer distributed file system that allows data to be stored and accessed in a decentralized manner. This replication process ensures that even in the case of a Push Node failure or network outage, the messages remain accessible via IPFS, thereby providing an extra layer of data redundancy and resilience.
