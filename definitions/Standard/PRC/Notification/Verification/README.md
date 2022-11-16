# About Verification - Definition / Specs

## What is Verification Proof?
Verification Proof is the outermost composable block that is sent along with then notification to help the network validate notification sender, chain from which the notification is sent and the content of the notification along with any other validation that might be required. Verification proofs differ based on the platform from which they are sent. ie: Smart contracts verification proof can be validated on-chain and smart contract based notifications will usually carry tx hash proofs while off-chain / gasless notifications usually carry eip712 proofs, though they are capable of carrying smart contract verification proof as well which makes it composable.

## Specifications

| Verification Proof  | Definition  | Proof of Verification   |
|---|---|---|
| eip155:chainId:txHash::uid::optionaluid | Verification proof generated from tx hash of EPNSComm smart contracts on Ethereum or polygon.| The type can be proven by on-chain activity   |
| eip712v1:signature::uid::optionaluid   | Verification proof generated from off-chain EIP-712 signing of payload  | The type is proven by verifying the signature of eip712.  |
| eip712v2:signature::uid::optionaluid  | Verification proof generated from off-chain EIP-712 signing of payload  | The type is proven by verifying the signature of eip712  |
| thegraph:graphid+notifcounter::uid::optionaluid  | Verification proof generated from any subgraph  | The type is proven by validating if the subgraph is attached to the channel and then the counter id is used to pick the message and compare the payload with the payload stored on the graph  |

**Note**: **::uid::** is an optional delimeter which if present along with **optionaluid** allows the proof to be uniquely different.
<br>

1. `eip155:chainId:txHash::uid::optionaluid` - This signifies the verification from the on-chain, currently Ethereum and Polygon are supported networks and it can be verified by resolving the transaction hash from the respective chains and make sure that identity is present in the block. **::uid::** is an optional delimeter which if present along with **optionaluid** allows the proof to be uniquely different.

2. `eip712v1` - This signifies the verification from the off-chain, the verification is done through EIP-712 based signature. **::uid::** is an optional delimeter which if present along with **optionaluid** allows the proof to be uniquely different.
    
    Note: eip-712v1 has limitation to support only completed old payload which include all the params of the payload which are part of notification, data and recepients. As the identity formats like 0,1 and 3 have single string payload that's the reason only identity 2 is compatiable with eip-712v1. To overcome this limitation eip-712v2 is identity independent.

3. `eip712v2` - eip712v2:\<Proof>, it contains payload that is future compatiable. It means payload can be dynamic and can be extended for future reference. **::uid::** is an optional delimeter which if present along with **optionaluid** allows the proof to be uniquely different.

4. `thegraph` - Notification can be triggered through subgraph. They need to call addSubgraph function from EPNS Core Contract to add the subgraph. The Push Node will pick up the same, verification proof of the same consist of - 

    - `GraphId` - This will be the id of subgraph. It is usually represented as `githubid/subgraph name` e.g - epns/epnssubgraph.

    - `notification number[counter]` - It will keep the count of Notifications and will process in a successive manner
    
    - `::uid::optionaluid` - **::uid** is an optional delimeter which if present along with **optionaluid** allows the proof to be uniquely different.

### Examples 

* `Transaction hash` - This signifies the verification from the on-chain, currently Ethereum and Polygon are supported networks and it can be verified by resolving the transaction hash from the respective chains and make sure that identity is present in the block. The payload either can be fetched from the events, add route or graph. This can be the scenarios - 

1. For Identity 0

```
{
    "verificationProof":"eip155:<chainId>:<TX-Hash>",
    "channel": "0xd8634c39bbfd4033c0d3289c4515275102423681",
    "recipient": "0xd8634c39bbfd4033c0d3289c4515275102423681",
	"source": "ETH_TEST_GOERLI or POLYGON_TEST_MUMBAI or ETH_MAINNET"
    "identity": "0+<Notification-Payload-Type>+<Title>+<body>"
}
```
2. For Identity 1

```
{
    "verificationProof":"eip155:<chainId>:<TX-Hash>",
    "channel": "0xd8634c39bbfd4033c0d3289c4515275102423681",
    "recipient": "0xd8634c39bbfd4033c0d3289c4515275102423681",
	"source": "ETH_TEST_GOERLI or POLYGON_TEST_MUMBAI or ETH_MAINNET"
    "identity": "1+<IPFS-HASH>"
}
```

3. For Identity 3

```
{
    "verificationProof":"eip155:<chainId>:<TX-Hash>",
    "channel": "0xd8634c39bbfd4033c0d3289c4515275102423681",
    "recipient": "0xd8634c39bbfd4033c0d3289c4515275102423681",
	"source": "THE_GRAPH",
    "identity": "3+graph:<subgraph-id>+<notification number>"
}
```

4. For Identity 2

```
{
    "verificationProof":"eip155:<chainId>:<TX-Hash>",
    "channel": "0xD8634C39BBFd4033c0d3289C4515275102423681",
    "recipient": "0xD8634C39BBFd4033c0d3289C4515275102423681",
	"source": "ETH_TEST_GOERLI or POLYGON_TEST_MUMBAI or ETH_MAINNET",
    "identity": "2+<Payload-in-form-of-string>",
}
```

* `EIP-712` - This signifies the verification from the off-chain, the verification is done through EIP-712 based signature.

> `EIP-712v1` -  eip712v1:<Proof>, it contains fully loaded old payload.  This is present to provide backward compatibility. 

1. eip-712v1 has limitation to support only completed old payload which include all the params of the payload which are part of notification, data and recepients. As the identity formats like 0,1 and 3 have single string payload that's the reason only identity 2 is compatiable with eip-712v1.
To overcome this limitation eip-712v2 is identity idependednt.

```
{
    "verificationProof": "eip712v1:<Proof>",
    "channel": "0xD8634C39BBFd4033c0d3289C4515275102423681",
    "recipient": "0xD8634C39BBFd4033c0d3289C4515275102423681",
	"source": "ETH_TEST_GOERLI or POLYGON_TEST_MUMBAI or ETH_MAINNET",
    "identity": "2+<Payload-in-form-of-string>",
}
```

> `EIP-712v2` - eip712v2:\<Proof>, it contains payload that is future compatiable. It means payload can be dynamic and can be extended for future reference.

1. 

```
{
    "verificationProof":"eip712v2:<Proof>",
    "channel": "0xd8634c39bbfd4033c0d3289c4515275102423681",
    "recipient": "0xd8634c39bbfd4033c0d3289c4515275102423681",
	"source": "ETH_TEST_GOERLI or POLYGON_TEST_MUMBAI or ETH_MAINNET",
    "identity": "0+<Notification-Payload-Type>+<Title>+<body>"
}
```

2. 

```
{
    "verificationProof":"eip712v2:<Proof>",
    "channel": "0xd8634c39bbfd4033c0d3289c4515275102423681",
    "recipient": "0xd8634c39bbfd4033c0d3289c4515275102423681",
	"source": "ETH_TEST_GOERLI or POLYGON_TEST_MUMBAI or ETH_MAINNET",
    "identity": "1+<IPFS-HASH>"
}
```
3. 

```
{
    "verificationProof":"eip712v2:<Proof>",
    "channel": "0xd8634c39bbfd4033c0d3289c4515275102423681",
    "recipient": "0xd8634c39bbfd4033c0d3289c4515275102423681",
	"source": "THE_GRAPH",
    "identity": "3+graph:<subgraph-id>+<notification number>"
}
```
4. 

```
{
    "verificationProof": "eip712v2:<Proof>",
    "channel": "0xD8634C39BBFd4033c0d3289C4515275102423681",
    "recipient": "0xD8634C39BBFd4033c0d3289C4515275102423681",
	"source": "ETH_TEST_GOERLI or POLYGON_TEST_MUMBAI or ETH_MAINNET",
    "identity": "2+<Payload-as-string>",
}
```



* `The Graph` - Notification can be triggered through subgraph. They need to call addSubgraph function from EPNS Core Contract to add the subgraph. The Push Node will pick up the same, verification proof of the same consist of - 

- `GraphId` - This will be the id of subgraph. It is usually represented as `githubid/subgraph name` e.g - epns/epnssubgraph.

- `notification number[counter]` - It will keep the count of Notifications and will process in a successive manner

```
{
    "verificationProof":`thegraph:<subgraph-id>+<notification number>`,
    "channel": "0xD8634C39BBFd4033c0d3289C4515275102423681",
    "recipient": "0xD8634C39BBFd4033c0d3289C4515275102423681",
    "source":'THE_GRAPH',
    "identity": `3+graph:<subgraph-id>+<notification number>`,
}
```
