# About Verification - Definition / Specs

## Specifications

| sigType | Definition                                                             | 
| ------------------ | ---------------------------------------------------------------------- |
| pgp | First version of PGP message signature |

1. `pgp` - PGP message signature

When sending a message, for this verification proof, we first encrypt the `messageContent` and then we sign it with the user's PGP private key. For more information on how the `messageContent` is encrypted, see the [Message Encryption](../../Encryption/README.md) section.

The signature is added to the message payload as a new field called `signature` along with the `sigType` field which specifies the type of signature used.

### Example

On the example below, the message content is `Hello world`.

Here is the PGP key pair for the message sender: 

- Sender PGP Private Key

```
-----BEGIN PGP PRIVATE KEY BLOCK-----

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
wBRozZKOhwwFcufqmoBwpATLuA==
=gK7u
-----END PGP PRIVATE KEY BLOCK-----
```

- Sender PGP Public Key

```
-----BEGIN PGP PUBLIC KEY BLOCK-----

xsBNBGMxvJkBCACELO5PIZQvNS0q5e8h7cjQGfh+IXLsJLBfhPEGre+Q8r08
G7e4K0OE5jNiGXXKYV+4YdVHwgwlxY5zCzOrbHCWwrNnouIhddbl2NVIJl09
pBP514vkAmxsUNXVpLjxWQC9yXjut1OhCHxfgfDz03G+jMrrZAqXLBQXmDxJ
zUPKU5X+PGz2qiKbOZ0BF+1ggPxP4ZMTuLs2v9O9Zhk+AllvLKFxYfsTF5XI
9Y0i9LJk7IX9dKYb0vfr3FbVTFRQIjdrvKvd+RU6zbheqWhM69uyUEMcxwzX
rw4hBXgd7zzsHL1KhLxpP/YktvKtT63nE35qNVvDuggbQF1Xmi0TFCLjABEB
AAHNAMLAigQQAQgAPgUCYzG8mQQLCQcICRBeEbVDt5a7xQMVCAoEFgACAQIZ
AQIbAwIeARYhBHQ+379eiEJ1zw1bcF4RtUO3lrvFAAAzewf+Lo5zOrvWNgj5
sr3XanqcM8VJLsm8O5XJVVla7yJyfBy+UgYlVBWjSYhr0dPX5VYSlV+nyCgx
zveLlWkD15b64NxTpPLwGvav+yk8S18GN/EUqX4WZdeouN3B1jUpWoTCLNHh
GyjBQn/rnQ3xN5SvGnSWliVNvR5unIvQAsDC7Yf8TCfx5ekpGWjuFGiN65rh
MByAFUeD5HhSjpEVUWaQc7cNA2hnYre1TDmFB8jY7uptMDR+6MD0LTvgApNK
G1sph7n5EFV4haPqNKtbu21MQqiw29MTaeCS/IvQyyzYb1lAAKiv+z4AZq74
+J0mjGVI4P9clcgJCBPb1Qj3WINrRs7ATQRjMbyZAQgAvWfut6Gk8LvQrzep
0eNz6VCwJ0gTwrogbHOxMX8r+Ft3MIUzAF/eKpAmUnhw592ubVFbBkNiZcG+
h6Xb4bf79kVuvBCgp52OqtG43HeTLfJL1WdUrJT3BadBXlIb0iWniRqx3ebZ
3a+KFNiDAMCLTl0ZRGjqVY/8vZ8UnOR3OEobqOgIJrCbKZ3l+BxLkBy2G+NY
zC0PuPr9xHu7iePUBjlGqDEaXNSwlFMVZDdae6c0C17wqtfCusYSY3/IO8nv
YlHO/0nxl6Vrjh4eW0mH1JcvwEEefkhMLlN+Os3XeBOxx1RhmWrHJPRTwCOS
MzvKaeYCsdTxhxIzXIehNu0gPQARAQABwsB2BBgBCAAqBQJjMbyZCRBeEbVD
t5a7xQIbDBYhBHQ+379eiEJ1zw1bcF4RtUO3lrvFAAD3QQf+O9IuYDDv/3qP
TICN8ymTY6rddVBv2GE3idiMfFfEwEoup8ZzGYjRWZ0bCVl823yw4l8G27Yx
aWdshasH+XQAAj8ZhjWZGHrgl+inqk4DAC1X1vn9jtgcRnaXYRsInFYDvGou
L0qkhOWutyF9Mog8cc66s473xKcY9NvK+jrlSzibCBWt9FFuZAZuYxsPwaFq
yWBeBsnkyDM921FFSxmxN9ZP3pG2qMkqK6/jZGob9HCf5oRYNeUbOmAovVJp
C2gzX/81K+ArvN0XrNvVEjZ2LcyNqFIw2Y3K+NLsthGiE1BdRu93hmMsIL73
MnC1wBRozZKOhwwFcufqmoBwpATLuA==
=63nV
-----END PGP PUBLIC KEY BLOCK-----
```

Here is the AES key:

```
oeE0kKQ22oHGmlB
```

After encrypting the message content with the AES key above, we get:

```
U2FsdGVkX1829XhNvWDq1f1CNR4yHfzQ1Dm79agXAek=
```

Then the `pgp` signature type for the encrypted message content above is:

```
-----BEGIN PGP SIGNATURE-----\n\nwsBzBAEBCAAnBQJka1GDCRBeEbVDt5a7xRYhBHQ+379eiEJ1zw1bcF4RtUO3\nlrvFAABfCQf+OTryGm59OOh8nYIvKHntnG9/Zc7ekPGXaKoj0GB6vEWJPq0I\ngYlDGWcBvU0k8drd7V9CAiG+d+TuoOnxJlLI/hLTy35W4hpvT7Pzu6e7Lqx9\nP93B2AX/5EGbi0904oCvLVinvGI7vmJlRwmjzvtZGzJdG9y50ayrJSM7uil6\n/l14oqIAb6hb9uROsxuEwoFZxBDk7S7WtZ7TXq9gTddJr16Sd5PwUN3RCBrY\ndV0BLLiPKwQz10CxEUlEElTpdJPMY0/Al9jNM1kZV89o/ITj8cILS+LhNFng\nPuSn6DC2WbgTCP3XJlpipzvqqPbC5pteN7pVxaLU1Sx7CMob2LlC6Q==\n=QQE5\n-----END PGP SIGNATURE-----\n
```

The message payload will then contains those fields related to the signature:

```json
{
    ...
    "messageContent": "U2FsdGVkX1829XhNvWDq1f1CNR4yHfzQ1Dm79agXAek=",
    "messageType": "Text",
    "signature": "-----BEGIN PGP SIGNATURE-----\n\nwsBzBAEBCAAnBQJka1GDCRBeEbVDt5a7xRYhBHQ+379eiEJ1zw1bcF4RtUO3\nlrvFAABfCQf+OTryGm59OOh8nYIvKHntnG9/Zc7ekPGXaKoj0GB6vEWJPq0I\ngYlDGWcBvU0k8drd7V9CAiG+d+TuoOnxJlLI/hLTy35W4hpvT7Pzu6e7Lqx9\nP93B2AX/5EGbi0904oCvLVinvGI7vmJlRwmjzvtZGzJdG9y50ayrJSM7uil6\n/l14oqIAb6hb9uROsxuEwoFZxBDk7S7WtZ7TXq9gTddJr16Sd5PwUN3RCBrY\ndV0BLLiPKwQz10CxEUlEElTpdJPMY0/Al9jNM1kZV89o/ITj8cILS+LhNFng\nPuSn6DC2WbgTCP3XJlpipzvqqPbC5pteN7pVxaLU1Sx7CMob2LlC6Q==\n=QQE5\n-----END PGP SIGNATURE-----\n",
    "sigType": "pgp",
    ...
}
```