# About Verification - Definition / Specs

## What is Verification Proof?

Verification Proof is the outermost composable block that is sent along when updating the state to help the Push Nodes validate the sender and the content of the request, along with any other validation that might be required. Verification proofs differ based on the state change. In the case of creating users, usually carry eip191 proofs. These proofs allow for a flexible and composable structure to validate and process user creation requests on the Push Nodes.

## Specifications

| Verification Proof | Definition                                                             | Proof of Verification                                    |
| ------------------ | ---------------------------------------------------------------------- | -------------------------------------------------------- |
| eip712v2:signature | Verification proof generated from off-chain EIP-712 signing of payload | The type is proven by verifying the signature of eip712. |
| eip191:signature   | Verification proof generated from off-chain EIP-191 signing of payload | The type is proven by verifying the signature of eip191. |

1. `eip712v2:signature` - Verification proof generated from off-chain EIP-712 signing of payload.

When creating a user, for this verification proof we take the SHA-256 hash of the below object then eip712 sign it.

```typescript
{
    caip10: string,
    did: string,
    publickey: string,
    encryptedprivatekey: string,
    encryptionType: string,
    name: string,
    encryptedPassword: string,
    nftOwner: string
}
```

2. `eip191:signature` - Verification proof generated from off-chain EIP-191 signing of payload.

When creating a user, for this verification proof, we take the SHA-256 hash of the below object then eip191 sign it.

```typescript
{
    caip10: string,
    did: string,
    publickey: string,
    encryptedprivatekey: string,
    encryptionType: string,
    name: string,
    encryptedPassword: string,
    nftOwner: string
}
```

### Examples

1. `eip712v2:signature`

For generating this verification proof, we first generate the JSON below:

```json
{
  "caip10": "eip155:0xFad30edeBA90EC446eC4148E74101C37b3bCc2E0",
  "did": "eip155:0xFad30edeBA90EC446eC4148E74101C37b3bCc2E0",
  "publicKey": "-----BEGIN PGP PUBLIC KEY BLOCK-----\n\nxsBNBGRYseABCACzV4wPnoFKqn49R1ASznhsRqz+13wRHUBWA2N2wpuJ9wBp\nfDaGm8KAr0M1lC8YW3pM5EB5dbgqYie54lV63Ghg5Fhu0b7puTL1LgY3lUdN\nyFjsz6I6KbKYWdmpKjcQ3skaSqoBNQLIYVKTk2w4yzlrn/VCXitnUAZDHpL9\nviwU2bS84CddUR10vXEQZ/sqeZT0cpJfJdsIdXeLLzFmiDAlCg1xXxalpl+X\nUlAGdC6s+IYbq6cd/GI7WVxUC+1WzJGZ7VMMODK+/V11ssfdLLwaYftKaNpF\nGthJ6JSE2W0Q7rx1yL1TH27j8SFmsIfvzMIdqA5kpTdbJ0QPCUDUHel5ABEB\nAAHNAMLAigQQAQgAPgWCZFix4AQLCQcICZANc5g1cHcBMgMVCAoEFgACAQIZ\nAQKbAwIeARYhBE3kIxo8N7eBrLPSVA1zmDVwdwEyAADlxwgAg+3FcUDHoyrU\nWQteq5UNmYLJrlEgY8lBNiWZat29eDP36cKs7l93jcHjN8xjUGde6jbFt2vT\nAq5ZKQ8Y3qb+HNLpxj0Ye+Qb8Iq8De6YNDMyfV//tkPL0z5PRc9+TMQA5QP0\np8wmAFdV4YjGj1/3vVJlwfgpk/L7bZLpbVhaqWN6xY9dULWGV1HpR0DXtI4N\nPd4WKtly5o7UVFsVzYObwBfksbkoLPOPSrunHgjR++i/pU3MtHXXGVStT8yb\nJSIcEwKXYVt6WWrX8nT6mXXhdHfyDG0jNqZDIiXuLCF+JpMLAExH4XOMVKd6\n9avMfFE3TmKJnF7v31BKBKZhamuTpM7ATQRkWLHgAQgAxEdWqtNLHYMGS/Gt\nf6gAXbH2GfHrWNwWT1D6i8G2wjsmTfrDHiQN3T/XRbfJKTZTt6dAnemWRxX9\no2LnJnS4wkyGYgwziVPeQIZgo0BB+yq2kZgKkGopkzqxErP+aAshF1l+HeCT\nkPBnfSkoCgRI0OH6orWLYEtFLfxpPzQXnzx6Mxl1hQPFKpdJh8lC9aPay8qW\nEKfF5BDGRXkLP1cCGIvGeLzTSvWCcLZWhhCdi94TQ4MuujWhTtoiQF6a83NT\nxx7cF+gVlDDeHD5FETn5drJQe9mM8ONXUEUNTLnorJzX8ggb0sYgu/kmyPRX\ntNKcGgJe2b/uNx/dQ8iBlaHyqwARAQABwsB2BBgBCAAqBYJkWLHgCZANc5g1\ncHcBMgKbDBYhBE3kIxo8N7eBrLPSVA1zmDVwdwEyAAB6FQgAiDWd1p0cBL8z\nCsk721ci9g3pIEe9vbp7Z5vyxcpF3Vmc+bO2zAg7ENIQgvLrkvrYe4QRg98T\nG8yXkRIn5sK2jvQtKzu4fCY9nImaEJGrjO3Dvz3oMhc0NiM9wTFjz/5TxTQX\nEO7pLS0gpHeWlhvKzw++wMqm2Nj9XlIVUVXriXqUyMvxedpRNA3EipdP1tjC\nC4d1erKn5b6ahnMHQkHFARCR+E60ZH3HyKiqDkNqGp9bK6sN2PbjMEqbugzw\nmK9gvA3uw0UfNG0F8HxHey5ogi+iXKAfAN98LMgyoYLQzmzxLmt6XQVTkLU1\nn25fX3HDl4lC2pXCK44AtEwJyykAWg==\n=QJRV\n-----END PGP PUBLIC KEY BLOCK-----\n",
  "encryptedPrivateKey": "{\"ciphertext\":\"7daaeb771050f7905c60905a14fda0070c6adf5dd34b9bc614234d23335e52c2d002da8ff6f54f99b622aaed140d5d0d7600d53bf32cf1088a6acf6732aa61e7d0ebe8419d019d77b9b544c77ad5dfe7777a8fdf5b552d1b7c4b07d43d5f068199066a0c20807dd56aa5cb4e4b2c12b274bd041ca8b86ab6fd48573740d75bb0527e30c97534081146773da68d34815d456f008d527078d837bed47d6b3198a704b302363dd07897d6701183dfcfd5a003f74975db85b9f3e6ce1f5b065408d64c43f92b95f57901f0b259aae49070a3b6d71cc21d11a10d741e175b9971cdb14ff78028d5f80bcf23f0c68dc4c40d8923ae8fd2c010435917f2a9d683cab4e38f56781c48f20d0146414a2dbecb868659b38ac2469b60ec48156c54a48916438d971c8ce981b9ee462986219c7139092f77c1c06dc355e2feb7a5cf5456887965a2d51c579657d209930fc55a46b283ed171ef93f69e011bbb4abf9df5e0734d9aa5f5e2e489f92c39606081cfbf84e8295e28cfe1edeaab9ccf7d64927c8821b0315b81ea89f4b215f19677abe5062a24f1c33ce99dc3b690b9df9c0765e073fc631501dcca374a45d42120b657199f2dd1417371b5e8a9b10b6535949b398c2d259160c5066eeefd121c706b161f810b8ce050a7fe50a6897dcdbf162ba0dac07c182bd8eda66be77ac8ac1b42f273b6b8d63c1510533375fab6a2f2613cd977507022668e984bcb393f017178f28b47ce2cba11f5b117cdf23e1a38dec08fb69942c28f61b524efe877e9b9ee91a807822168fe340c9bcfbc3dea18c3b04dd48902994bc015b4227199aa7ae89aee3a771b4a28e5cf0c3cf048095e47ddb8fb91aa50bc4265d7dbe18d263d342f290a4417ed578840620db447f427fab9732056d4348acc6baadde64ccdd94f61205163f736480dd0c595cce23c2762b6a5fe1580caa4ff866aa085068879287814be973613c73d00e299be28d3106e301878c15bce8237148cb68df3b3d24a0aac6d14bbfd64f78fcd93051ec898fe80ca01dc85e51778562ffd1e7c74cab09a2d1f9c54b8b588fc6a06db81cfdd26fb791849f38bbdf085221ed3d8b78cac6022371140c3f7f4541c557930dd4dcd2f02357f95574bffd0019234d8c88aed37161dd0c601564591f92f464af128ee3460b9ce970fcc9295a91eb1ac7db97b2396392181693eae1f556b24867575a7d0212591a1c467c85f62736282843367456994a06f198d439f5eca24558b3647bad1ebd4b1aa75535866573195454a5581521c5f0117dc34f38f10a9abcace07ea77d5f611d318f3de1de0327251121e2482e8f9cf527165b5ac4c9daf1d748ba79540cbd0ba0e4c5806cab3496e385235be8653ad271c31f8ac9d48fabe676c81a6be1bf6a239966da88db2c5a17839891c0d2040ed7a2cd9cb205e9c26e7fd6c819277146e981335b6dac005a5f00df5a443e15e750d58f97f5610fc3f6c94e397ad7f4ac174de62995c4bfd41881fa2e35ad354e726695c3bb4fbfb1fcc0acb7aa26b2a8b0570b2ed0d3603a71d2bd69683e43620df8041d9ceaff5131792bef57ff7c4d1239508cede2dd968e616a2d4e457090eede7cbb77b49185a472b725d2c9cafb85ff363fd70a454f9e9bf861e28e3689a3432c6318ed380b38f1f03170f0ef5310e2839d4e3181341ce26f1343486a73e4a16c77e25569dcb5f2046915311ba1dd7a3d6cf892caf342b613c6d1555c32589a32f676f30adef1f281449bf4246b29d922210ec6b048998104ccb9e242b46a0f47b880c7cffa0f6dd4e4408391120d92dab5bd6c3816156d5eaed03e0e34bf662907547d809401a25c597c293e90251ae714f9c8f84c6e6ee419c5963faaec0445c63c1fa43352a13a55afb5a0c8dcdeff1f36e49fdc479bfc96138a40b5b04cec938ef628839e4d02fd3022be59c2d1723362d19c02f9a24ff34fe1cdf9705b8201751470afc91143fa68d9f12780e4acdfc99a2c5f284e6c6ae1af58411f4df8b394e684e531adfa4ac2dcc2d179481729601adae8aa8eb0da030ac899cd49e6e027ebd068c8d0e2b7373c9ac3cb704fb6bfa3085f4ef526528fbdc4e8cf4d9deadd2aca49316f4d27eb4d5c62ee34475dea36b17ff1cabf025eb6b1909f7b9a746da3f66f856dd579edde9115fed1a0747fb7524cf7a8ba0265a520c6b237d28f22727472b467e7b75bb8b97055fe02bf5428d6ee8602385ae708abfef17d8786364ee4bcfd5c6cd639e7e1874b4aca8a23bb62e556e1af86a0b5a8c8f9d2f6cc50e294737185e7d60f6707f61f3d66ac5a1407cbf83a8be221edd18f7c2a28c889c98efd8874a32f18775d0e97ebe0433b9e6843be80c10e1a760da681dc788740b9a3be5611c730d2d81529e0e903f5cbebd4137ea2f4c4b4a5f1477f7b0724110a5e289ff134565cf9578f1673bb397653b1312834a1eb641beca725d53929dfba39133b3c79dd049fd3f39ae3874656d1ca5820328afadcc08a77d2299aed0325796f31d934cec0a9cabd1e253a4ea161c594973a180113665a33c9d8e8b45057cabce4eaa9c680ff01ce94b0779cc1b52d9440326cc03cdf8d81fdbd878a2a47bc9b4a1ecdf38fd9e9665eac77a0a505c3fe1eb3f22bac6673529ef1763fbe2663c4ad21f9162840480852d476e5af70b87616dfdc6eb37bc1eed44828809d586d2fc640ac653e5ee7c3278ac3f6319efd48dc347693ee88130898e7c2eb43beaa878a50d30044042fd051658b03be83207dee36f2ce5d2e69dc3c0ccd5c13884b6e3ce2ebc772b98288a184dba5d366e834597ebf5b50c53308d5350e39053f3aa7aa3848abae0e865483e16efb8bce43705c1aeecd55a7aab572feed54586ecd75cfca30de77dc4392f6f1329ddf7c2b904e0037ba1df9fa353cfc452845bb44b1d6b5a573026f8db28ecabf3ab67df6db783c2f82b0570e0ccf0f4e5a093a66aa30550f47a27d488a56fb36697aff88eae85fd4ff03cb4c488587aba8436f93b3cbb95d7a45283f117fbc05a6238eabb4b8d7a308fe396e9b75d6a5fe3220d3e3b75531f7f299f45bad43691c6f3f76a1210146152ec5f8337a1268e11f989a4abc38a725ff1177229b8e78597906b5de2a018a3a34735e2efca8d9e16162309cd5942339f23daff8929ff9cea6241e3ca76dc651b6f4eda8427cf4365f12fdd6d20097e06358699610f71ce87d0f2efc89cdea694d543fa0df503141f8ff76ec7863427e8c16db78001ea976c720031473caf1de9c3f9eeb503abaf9f96f56de18ab8c00ad87555e00affcd256ad1828561559420bd2869edfb7116aa7e506a0de2b1d674ca4eb25c1226ee8f875e60f529f6bcd5dde626b14cd76576d67c454004739cd67fb1e97c17a9f791a037d702063a5ad25b0192c87c77dbc43f29f28ca221ff953dfc1d84ed02fa2799bacb5dab6ad835f89fe62efe6dc2cf82d96577cdff964aa5657e117c60bf1aa96188afaaac665d0fb61eff5f07e0cdc4020ba33cd9c46aa2b78f548478269f5a1063c48dce0a51627bfb1da0726030f860e8e63d46e09d2ae50860b13d540853967998fa128d912539f49d0aa1a1cf8719a401a3eac9383da8ab0bc04b0d0f9b055d2c4ff2c05aa2a1077e241bba92e0061f2e42a9b4af15a79a3ae299bf22b972716694bb66f6e257a37320c56c787eae73d9efb8ba557c5dc17808fd44b8b6830b270524a6a4d8abb95ff3d64431baa25480e7f9f224732dbc9485838a5e20c3bbcf0322acb1ea079ce116c189ed3dca6991cd880f1260f09a88684c2ed911ccac0ab6feb599fc86ef268a10d2e58a8d7c3c09a9a890dfe5e5632563b725f48cdcbe87238702ee059916c52327c43e8fc16f9f24c99baee16a346eb6ec891efe8846179f72056147ec9dfe944c5bb233965985c38bce5f6839e233c7c19233f2979d25df3d64daac19325a027d7cf8bdce8c4f756ce32b0aaf041bec5a2ea613488434a5040a13347b8648e38a3819a5930989bc43b18bf490f6d3295ff951b14d3afb9d09fa83ecba31fcb3e633b8bd0d380e097e4e45eb3d7894b6764e40e9a233c99a62a3de57b50443533b68d649cb7fa42c18e2241bee72d685ac93fbe4d3d1116d3f1973d113e1fee52d8c1fbf93dead7a3df8cb1d49aa6c9e834b5f465b84920b3c399d97fe30c4b45463d3b80d616efeea3377828358822987d82d4a4a73a8242731699e7de258abbce25af1d25837cefe41d5f6381007032ed845817ff9d71226032a4dbab7655b28f8343fc091644d65ebe31a4a6f0503ce7e21c2f25303613b03d9d930610f01dc40d597ee7af159ed150856c60d89717c5d33c9996dabbc05759a2f0e6a57d3140ed4e4bc890842e53597f33e956e82354e0132f47f1a09805f880333e4ffea0fc81fa8148ed530e2f5a2055b6680269b434186d8e757a5b7f53124b8e36f5e55fde382f02dafe7ee7e17e2eda31eefa4440786b9849b732a6ed3e451f917697943ad6cfbc1ede4ad902d4c900183620344fb7f00b013c800029c95e24121b40ace9a5dce983ea77965f2722dcb2828df94a2e21f9df2b205d47cc5399c5ec5e84d5e6aefeed606a4aa05b0ea6dd1bb2202905e437bcc3e049f98478f1814e3d76e07ba339b2cf033f6035444995c1dbb0854c6c1ba71ae2a42b28502a46741fded0b4c3837711c13a569129a8867e056e7c22723877921d509fd9314e5adc5f40aecaf500da64b2bff854e7548755edfc9794da2b62cbcdd24a4098bf95a3a97dafce543ab740328e92049feb4e6120b5677a2c68fdef03205e930fae9c283805f7c7d1f5700a69d65148572d401b2f158b0afac742ed0b4f8164fdd6ec80a172e76d1d5fb7f420216d55cca8dd11444e031486d48ef6ab33fb97e99b42bcd65137\",\"salt\":\"8ced948fe77075e789364c410f15e74d5ac1164b64dbc54ba40be9b18780f636\",\"nonce\":\"5e7706c9e812e36ec6806126\",\"version\":\"eip191-aes256-gcm-hkdf-sha256\",\"preKey\":\"26741dacd90412b1c276c80731ab61939be6211da8741aba9240db40a90f86df\"}",
  "encryptionType": "eip191-aes256-gcm-hkdf-sha256",
  "name": null,
  "encryptedPassword": null,
  "nftOwner": null
}
```

The SHA-256 of the JSON below is:

```
f6c91236c48797deb2e330242862c510a0fc8dadd479041b7b507899d4ded90b
```

Then we take the EIP-712 signature of the hash above using a wallet with this private key:

```
0x5c94c6cf5f338894339ee0cc4f60b02b493e9ee69d0a4c27c719d17d44cf3cc3
```

And we get the verification proof below:

```
eip712v2:0x78dfaf4f86d6a8583b61e5c1a193fd151bda74decf206e6d8f91d764109d2b0e0687f0c5c28c58d746e74edc6742626fea02c118b46a4b87f0d4835b9e1645471b
```


2. `eip191:signature`

For generating this verification proof, we first generate the JSON below:

```json
{
  "caip10": "eip155:0x3E3D52D24b1D96cF275e4fd8bc4F5638Edd1fe51",
  "did": "eip155:0x3E3D52D24b1D96cF275e4fd8bc4F5638Edd1fe51",
  "publicKey": "{\"key\":\"-----BEGIN PGP PUBLIC KEY BLOCK-----\\n\\nxsBNBGRT92IBCADDYYObUwK+dPmGzzEZPBWhzAM/cznZyy3StJhaE7uFBXlP\\nktBsoDr9KYmoCmbqVw65Qpaire6x5Y1e/U60/BpFgTtxH/fCHGRAcmAcAf40\\n459hmfhX8g4U0zO/ShBV1Up+9bsRB1ZBiiKE8YtOeTF7UxIx32jhjmDLJfhj\\nivRxwUv7Q8L+tL7V+7TE/L8r8/msYk6Ex6RJVDkVf9OlSJ7kPbBypFbSRaFJ\\nd9DY/tVu5I6rPJMHkhdh4MIcCxxZKLnYcNG1YzE4QW7ZFBpJLzsGXMlMY7AI\\n4Wwx0nvfKTRCeFsrI9ZUDEu6gd0uU1+z9fHGHVW1uy2UIyQMKhFmJrtxABEB\\nAAHNAMLAigQQAQgAPgWCZFP3YgQLCQcICZAOd8K7O81EfwMVCAoEFgACAQIZ\\nAQKbAwIeARYhBKekDJE9u2pk4A+sHQ53wrs7zUR/AADmugf/eNvYR1CnFbbN\\nYGybgK4vIaJ4tB2PZyUvFUgFhiEtGbRezJtCIn4v4QEGIKvvmxca5GjzVUy4\\ntaAVP3NqX+eCfJXONdhixn3F2YNDDSju1v0Z1XIrntPP7PGflNwx/HDXq1dP\\nKAYVz/XhlJlOCLdNUp3qYnAI1p2FwOHfKUidOeC2q5B8tijZHp0DMgkhqXBf\\nR7yFryBoBCUyu8n7xUVaTpU5Zv4jiajY/f/gs6RBRFS+vR83CJMXm4XKcWn2\\nD0Hdmls1+WS/lW260YF6HeIzGqgVaGeLTUC2wUMiUp0JBtHQTTdI+vEnfDFh\\nhDPnRVjPbs32/Btpq2EXefFVKFaTFs7ATQRkU/diAQgA7K4txK+jduioSHmm\\nSGK9WHgKtdgCOqHAZA9ud262iS5f4aEDrn5yrkm+IzRm32V4qZrvwyogQUjf\\n69YBjhSB4DsNON7vLeQnfvjoKGoc48t9ditrXRBKl6MCVcoSIM4W3HCmapR2\\nqzH42R2grPa4kDrmS+YISq4aRkBUFRRJ8M0joZhcup5iJfWGvDTg4Yd7ntOH\\nPCxTVq9nLxz52lBidPawFD678yMrP6H5TmdBEq8rWQPCK3aF6fTvk4qgK6xd\\nOHeGT/LNwi0ZYcLABzrjJ3BLCkNWYSkkb6lUOw4D8ybIFeTuq6AF7SRysqs/\\nONfF35a+TCXsWvYHcZzqptQ4oQARAQABwsB2BBgBCAAqBYJkU/diCZAOd8K7\\nO81EfwKbDBYhBKekDJE9u2pk4A+sHQ53wrs7zUR/AABn0Qf+L+LaoUIyFAYg\\n2XePeU0UeBvY99l+mp7GhGpQ0HtWUs6yS7khGg+rFjRBSKNUSbtZVJzOkzVl\\nsE1IfjblyexRnlnk1qmKETuYPVGR1bMTZleO9iMjrohE+/NSl1HNC5ZMOMiL\\n2HHBVcDHZNVgq24mnt37lusvOU/5MxxuubIstiejapnu0fYU4GTHwD2BNiH/\\nYb9R3XExYwZMREtr9QrZgUrFXY/pUsxugLE1jxLh2a6vbd3lTeiVXF5CUJe5\\npM4TKZ43667CJkHH2ebPCvpdLjmApsk52Z9fZhAxJw9xBYrD4Xwt4VSbZYNC\\nM6W68qhpO52JLKexdGhHxv2lf9t9Hg==\\n=AWPc\\n-----END PGP PUBLIC KEY BLOCK-----\\n\",\"signature\":\"eip191:0x10dc44a1395f85acb7dbf2222ab84574e2bcc1880e31cb5b643953e1943cccee034b04da1f856009604b1cc05b6b8c74ecaa774d51d769de93e1336b2093ed831b\"}",
  "encryptedPrivateKey": "{\"ciphertext\":\"c7465deac68328c5ff32ddf6242aa3765df065b507403f88135d5509d189062c138a8a1cce6a7b375d569214bd3e821a25a472b0711c4ef3792eb941903801800db0afb5c2fbf3d8930c70901348d549ffa57f3cd6da5839a3df471054766688b701d43d5e248521c45d19f653d035467b6c3b165cfeaab3f4f1351251e1879f33776bdf7d0b52f6130584bb93529a282029200c757b630e3f87f0cb438a1a48fb19c13e0ae84babcdbdc6c8d78a3d4c941a8a8803e93d6ace71c70ae076e1c54d9f45caccd867f7eb2098d055aef765ef61bc585f777a0194199674ec04d7422d5271dd3736a11292a33431840be1cfc40440d41c825ac0386d2acd507aaf11c74156f15d3f61efb24412bbe65caa04c525d048ad1fde96bc781588f9e1967fcfa7f83f054166053efec00d0d1c8829a6f0d7551443327967dd869f64ec20e251704f08f49511b3445f9bf9b1d8c6fbaf6f2f3c73056e9e48d151d5e30b84034e7906d6239ceb2c50723df99e371c931d069ab838338071b03117a4276727b73e471a4daf172ee62b9dc12a1309645a9809b91b154fb9139797ca8ece29cfa6f960997e1eb7f530ec05f191acb0892c948f4f46d7142b7835ff6c6ee188c7caabc10343d287eeaef7cbc729505f0a137101d2665854049e57810f395114da29f833f6f65dacfaba6e97b4df31b38f375c0caaee09fbc02aca9c2f66f5b39618bc204bd129463a12deb1c925ccdbc96519971f241fcb485c04a7bd7eb641f8e744da21bea0d36a2dc2db62b94583d7a9533a6f3242641f282f65167a751a3a95575fa4c40862474d797249e1dfbe54a6a4f99910482f60fdfbf4ef5872c387f9813c96694d94d04a2010d76c9da2df65c2a62fe4d0b958ba3d6838538405f1fd3c9af870c0dac68b76adceb768462cdc9f00ce0d724e6c1e97885886237e743de776916548d1205540fdae735631ee17bc5ef641f8799151c1e693436cc1d53e944f69e0821b56106f478bca79ecb6286b1372df43ed4a3ce073229395cb8b387919fee8b2ecc32ba29ede8271b943142691ffe8473e2a594e361bdd8576bf4601787d35b237bda2f0564d67aa2f60eeb375b52b2b6154ccedbbc2e404b4b9326690ac9d398bd6aa53212bbd78a4e2461073f90b007ceca3bc789f33a6516e23266c04383b7fc812cff1f5574a516adb420ecd7b4d1895aee58118645167a97e7216420c1e5a2d7ffb77f744fa9c1999400899c177bb5b165312ef265edc03349af8daf14f4160a7af31b75451150e3da8ccebba5db6fc4e92c963ef0f8bcbcc815cc1d18c7deea719ef569dd59a16ec7597966133437589592a594065ea15167cae608566e16cdad9e3b3bdcccde4d89a7dceaf8cf155f5c34fc6994016422e50e74dd4d4be44d8357d1bab3ecf263399d428605f9f0d7528410657a1dfdd6ac32e3184397d0677695dcad46bff065ab6db432dcde97784e17285d5fad7eac828eba0f5835662220a14a7893c6c53c283c2c4c217e8770dc4b3d322b207fed414dc354279da21750195e2d821b8dae4e45f8ad8e8f917f46b4cb2833660fcfed59b3e5c998ec7c2b82b2dc6283e5c5b3c6a3cea7089e80400286c980afdc2852b7cf04dad0defc647f0c91ab057a43b002c605d447dfdd186c6b81d4ab6459c230d0dbfa56d8c4e7e898d66b2b0b47aad7fa3013fa3b92a121dd6fdf8eab65cc48b47997c9fd3eeee0ef5f61e6cb3362b61d07b60cce878bf934b5745902aebfb8e8b50f16b6ae721ab1276d9e894859f7fa0e374097bcfff5d569ae93aec5e20465c5aad5ff89ed6e35f71159ffb4279e3008ac4616dbad7f5058f6108a26699abaeb62e6d83b332679acac2010f6e5272a81aeb968d59bdc30996c8ae0022bbf5b0585623dd4bab9a12707c658e3f8355ef3a41c7e657c72614c464c4ec6ec187a132e56b875a245e9634e1181d23ad18d8e6c722ec9c57182e548ea39f5954c783492ce8218d1e529d3cf3cf84b0ee9e440e5fefde4734d4e003eab83f500eaf526f8a695df011df02fa3a752835458ba28ad4a7e63eef6fd63077d52a93bf142741d542752d430822534cd07df4f5960b654bede3f9dbe461d022771ccb8df8e6774295a8407cabdbfe1abf7d1437784e458a2583194e8b39bd09b4bacdacc10aa41c0e03972b337d58439de868f27e277633fdb0162ceb5f95c2c774be15248d5140d25f46874e74d39f4e5105bb5b3c7d9b0454c3137ad75a183f58fa64dcd892a0515e482e74b3271230da09f94980ad77a4ea1be85b45037bafa6729d282d620ca2e37c2ce9f68f1e11285c1d81bd464a3191d7dfbb10ac82780d971007b14614bca9688c957973b3931028663aa0f5231ae8e554932266d4f312f22739dec983fdf22ebcc9a1b4867304e392767b00276b7c263ecaac19ec0fa9b09db763127ce9e4e98687c85d892e9cc5545e59037e42936f9357ac1a8cbb73bacf30cd011dcae533febc43ab24bbf55b3aa364f7dd0ce2975c27ccdfffb1dbda26f90a8e7bd944a2746283cd139424539cb5f958804d2f5326fd2e6d54189c5a39560f417688d0518b06aeb1c8fd4a95cff62ba72caa16be1e76d1ba5ee67ded8dada16102f2f8bb8a23d561e7a363e12cf30b67088083dc1d38e040c9e0a2df03bcf65a9a8937863624fd1fbdb0d4db68cdeaf00d13e9e745b6bc7ebd9fbbb6f6fb004dd2094ef39105d54f75670a66de19f31a28cbf18f27627185d60458a482ece43d52e7b1249be46cf8d3fca80004a3826540816c8435d6ff7963eb906900e20250189043d362c2574775592f55125948581ede19a3bebb21794cbe7d708b52c8b83493a74a312737e2eb5aaae563d25c42b10b7ba98439cd4d44cecd2302436aea8c833f3f3d559f5c86bf427c1fd23875a87d0cad78612490527a12e82fa0ef1159a697e715875e56bed50ad3b6ce07b00729f8b00eff8563697c80916a050c7de07adaf8d5f6300e83480bfa15484e7b3930761c95bf9f57542990c3e0cad7c250269e494faa1f3e7048c67eb6948c5448f4c01c08074a941b52186a78d7fe56117e6ec869628ad8d162385c0a4c9e064ae71f69ddf136a92220ce2911f18af20430c473c985ed9fef1037d2d206555e4e01fb0a415fa50ff597a64b7dfd81d89829838587c278dc19c3378e8972ac11e73c2bbf8ab65f32180cbb3396ca924a7248e401c6a8cc495e575121784ceab8e30ecb2689fdfa8af09f653be8f643ccf6139177da7337c5139e966ad8ec5f0293ebbe8658da40d5dc81ed5fed0d726e8559b78d84aaaf97517984935abfc25178a48e572b9a6a188dbdb58177b0ee05e9ac00bf17f35d326231aa51f1f6646c7d0cb87dfe6cda560ca7d5e096a5fff58d166147ccfc68c85fd47b6b1627f37f4796c293e109f5ad15c8454549a865ac1080fb76d1121039891f348f395b567474a3e7adef0057b181fea9ab2d0645b7cd3a6e4a6ce2368068ac82a0b89a1cc204beec44669c06d53cb6eb67e9514e0bb27ecb7182c24262ff88c14cd2ecbe37a3a79857773ad6a52d9bc1381218593a4ee9603c977ed74a75773b0c9c4644489da137b9b9e1c148279e528997d2c5926296530959fc77021133663ad3836b219f4296f1ac81c5297c061261c8c3fb2de1f9c786bb366030ecbb4c7d401cd020ced38ab9d6a2d534853d1db42e902c6eb1983178f69c61c69f70130190f473f88ef2c71d163c0c1e487d1a1b69eefd3d5ee0e8c3b37e0349ec3598e75745070384afb0566e26e4b43cc4b12c1d38d45bbf9833e4ff4ea1bd4e09a6336e862a40161075a94e45f119c47b15e8b5365762e5f916ba5ce3fdc873b1be1240b50936d4670507769fc9fff3f9b2ee505784a8a591df5bf8fdafbbaa0ad0b21f5650feefc7850ef63a6546a2587bfa7a8b89b17fce5d28e5e6ee9fa8e1eb1fb1273fec53c0401573dc4cf8d52b7d10ae3cad0d6f712cf7361dc79aa2fcc4e071e19de33f326f6ba90c303f309d66969756b3a34358472553a6ff52c5b1535f2d8209d4e7695293fc4aeb79a4b6006f7fbb2ed4f83aab799ec647935a53b3bd5245210dd173f56053cbdb9c1c1cfc393a60030d88ba34e4033b60b1265256c66811f25e53d92e012e1f303ad1322e7702b7c83db259d79860e78ba0a087c1ff038afbda2b833a9adda6ae816cebdb7df039b7aada5b45bce27222d1485437ac8663ee4f756ce0d287835e014cdc1c9a6e1e56fb6e455a8545ad1c0c51d4d116fc7d41ac401ed17f10c9632949c12f37ead415d1e2fb4fc757600c3f0d88bcb4a77d9667b85c3912cf54d870029714eaccfff3ed87ed64a5696c877b850b56c9922fe746e1c36d971095d7f6d6720f959bc41fe923a269128e96f30221a093d42a1bc5245977a8489b2ec4c6c3fc75a4f301251280ac03f815ab9f34fbec647d9adcb2870d8cb126de8717d9870bfbcf153dcdda06fb6ee08a639ba11b70749a69470ba16fd910cb363af7cdca8bf51484477b1cb9328101dcdec1154431c9d7f3cd49db7b1b916d1b7aa526f68f3bc62f8810ff4d38f9bda33510dbaec4db116c2e60cbff1df3a0022c1b1b4d780a9f671f98c27feb0fe9967c08759827dbb25f3c8dcab3cf984ab2b2a7e789b97c19c7ae483a3e771d7f41b14996f62d5e48666c29ecb5270b702a0f32189005f2bd6e66050e141a1cd1c9aff7cb902f42b9c1a85b48b09b90dd7b4fa37fb8f5c41a5ef96f0896d6df6f83395a910b99536fe628e4a83dec574125013e50c8600e06c88f0802bdd9c87556269ccac616428d3d727b5086820e35e2f853e8cd67827501384ac6dbdd674ac88164bc255e5b0e05cb18bb55aaf78184910d1cf24eb7b2bba63d0f681fedf32618a1f6e3905cfb1adcdce67ac69e4af8\",\"salt\":\"f0714db48256fad25f38c0f8e8f12fdd1958a9856657ce56c313308a671ef64c\",\"nonce\":\"dbbc53ca498420eb03b9e181\",\"version\":\"eip191-aes256-gcm-hkdf-sha256\",\"preKey\":\"348d42f2faa246114c8c62c75812cb66df873d5bb57e8ec106974871a08189ee\"}",
  "encryptionType": "eip191-aes256-gcm-hkdf-sha256",
  "name": "",
  "encryptedPassword": null,
  "nftOwner": null
}
```

The SHA-256 of the JSON below is:

```
9c5f42d8842845e64e1c50c59f487810f78d3063153c7a77bd8c2a453f248518
```

Then we take the EIP-191 signature of the hash above using a wallet with this private key:

```
0x25d2c7144ca6ff91412f6c7340f9c352e4eb4bac283b4a1a6195cd6e97ea58c4
```

And we get the verification proof below:

```
eip191:0x5b614e0f9196f0982ef4cba8381bacd128e6ab6eea2f34f28ae682c0dbb655fc433068ce7fc64e9da27516f02377eb887aad50ab8240339f670c62cea16d8c961b
```