# About Notification Payload - Definitions / Specs
## What is Notifcation Payload?
Each notification sent to the protocol is essentially a JSON payload, bytes data or hash / pointer of the JSON payload. The protocol distinguishes payloads content which will contain the content which needs to be displayed, rules to display / morph the content, the recipients for which the content is meant to be delivered to along with the encryption method used if the content is encrypted.

<br>

Notification payload type for Push is infinitely extensible and opens a huge range of possibilities including multi-factor authentication, payments, blacklisting address (Multi-sig contract as a channel with exchanges as their subscribers), etc. The data defined in the JSON payload they carry is used to interpret and extend that functionality.

**Note** Due to Identity Type Minimal, it is recommended to not touch the order of invidual JSON object but add things right at the end to maintain compatibility.

## Specifications

```
{
	"notification": {
		"title": "The title of your message displayed on screen (50 Chars)",
		"body": "The intended message displayed on screen (180 Chars)"
	},
	"data": {
		"type": "1" or "3" or "4", // 1 is broadcast, 3 is targetted, 4 is subset
		"sectype": null or [Encryption_Method], // for example: aes+eip85
		"asub": "encrypted by secret using sectype | [Optional] The subject of the message displayed inside app (80 Chars)",
		"amsg": "encrypted by secret using sectype | [Optional] The intended message displayed inside app (500 Chars)",
		"acta": "encrypted by secret using sectype | [Optional] The cta link parsed inside the app",
		"aimg": "encrypted by secret using sectype | [Optional] The image url which is shown inside the app",
		"etime": "[Optional] if given, notif will be deleted after this in epoch",
		"hidden" :"[Optional] if given, notif will not show in user feed",
    "additionalMeta": {
      "type": "contains uniform data identifying the kind of data present along with a version separated by `+`",
      "data": "conatins the metadata",
      "domain": "[Optional]"
    }
	},
	"recipients": 0x0 for type 1, 0xtarget for type 3 or [
		0x1: null or [{
			secret: [secret used to encrypt]
		}],
		0x2: null or [{
			secret: [secret used to encrypt]
		}],
		...
		0xn: null or [{
			secret: [secret used to encrypt]
		}] for type 4
}

```
<br>

| Payload Variable | Description|
|---|---|
|**notification** | [Required] Represents the notification typically delivered on the home screen of the platform (mobile, tablet, web, extension, etc), the icon of the channel is automatically added to outline where the notification is coming from.|
|**title**  |  [Required] The title of the message displayed on the screen, this differs from the data json because the title while transforming the payload can be different than the title presented. For example, secret notification title are always transformed to say Channel has sent you a secret notification. |
|**body** | [Required] The body of the message displayed on the screen, this differs from the data json because the title while transforming the payload can be different than the title presented. For example, secret notification body are always transformed to say Please open the dApp / app to view your notification.|
|**data**  |  [Optional] The data field present here forms the visual feedBox for the user. Indicates the data field the payload will carry. This allows the notification to transform according to the payload type and the content defined on the platform frontend (ie: app, dApp, wallet, etc). |
|**type**  |  [Required] Each payload has a type which tells how the data should be interpreted, this type is mirrored on the protocol function call as well. |
|**sectype** | [Required] is the encryption technique used for the secret/encrypted notification. In open notifs it can be entered null.|
|**asub**  |  [Optional] is the subject shown in the feed item.|
|**amsg** |  [Optional] is the message shown in the feed item, has rich text formatting.|
|**acta** |  [Optional] is the call to action of that feed item.|
|**aimg**  | [Optional] is the image shown in the feed item, this field is also capable of carrying youtube links.|
|**etime**  |  [Optional] if given, notif will be deleted after this in epoch|
|**hidden** | [Optional] If given, notif wont be shown in the feeds
|**additionalMeta**| [Optional] Contains additional meta data to give a more personalised and contextual data
|**type**| contains uniform data identifying the kind of data present along with a version separated by `+`.
|**data**| conatins the metadata.
|**domain**| [Optional] conatins details about the entity for which the `additionalMeta` is defined.
|**recipients**  |  [required] Recipents address needs to be defined depending on the payload type, if 0x00 is provided it will represents all the subscribers of the channeland in the case of secret payload each subscriber address will be mapped with the secret.|
|**secret** | [Optional] is required to encryption and decryption of payload data, this will be mappeed with user address as key value pair.|


### Examples
## Standard Payload - 

Notification payload type for Push is infinitely extensible and opens a huge range of possibilities including multi-factor authentication, payments, blacklisting address (Multi-sig contract as a channel with exchanges as their subscribers), etc. The data defined in the JSON payload they carry is used to interpret and extend that functionality.

```
{
  "notification": {
    "title": "The title of your message displayed on screen (50 Chars)",
    "body": "The intended message displayed on screen (180 Chars)"
  },
  "data": {
    "type": "1" or "3" or "4", // 1 is broadcast, 3 is targetted, 4 is subset
    "sectype": null or [Encryption_Method] // for example: aes+eip85
    "asub": "encrypted by secret using sectype | [Optional] The subject of the message displayed inside app (80 Chars)",
    "amsg": "encrypted by secret using sectype | [Optional] The intended message displayed inside app (500 Chars)",
    "acta": "encrypted by secret using sectype | [Optional] The cta link parsed inside the app",
    "aimg": "encrypted by secret using sectype | [Optional] The image url which is shown inside the app",
    "etime": "[Optional] if given, notif will be deleted after this in epoch"
    "hidden" :"[Optional] if given, notif will not show in user feed"
  },
	"recipients": 0x0 for type 1, 0xtarget for type 3 or [
		0x1: null or [{
			secret: [secret used to encrypt]
		}],
		0x2: null or [{
			secret: [secret used to encrypt]
		}],
		...
		0xn: null or [{
			secret: [secret used to encrypt]
		}] for type 4
}

```

### Reference Implementation 

##### **Targetted Payload** :arrow_right:	
```
{
  "notification": {
    "title": "The title of your message displayed on screen (50 Chars)",
    "body": "The intended message displayed on screen (180 Chars)"
  },
  "data": {
    "type": "3"
    "sectype": null
    "asub": "[Optional] The subject of the message displayed inside app (80 Chars)",
    "amsg": "[Optional] The intended message displayed inside app (500 Chars)",
    "acta": "[Optional] The cta link parsed inside the app",
    "aimg": "[Optional] The image url which is shown inside the app",
    "etime": "[Optional] if given, notif will be deleted after this in epoch"
    "hidden" :"[Optional] if given, notif will not show in user feed"
  },
    "recipients": { 0xtarget : null }
}
```
<br>

##### **Brodcast Payload** :arrow_right:

```
{
  "notification": {
    "title": "The title of your message displayed on screen (50 Chars)",
    "body": "The intended message displayed on screen (180 Chars)"
  },
  "data": {
    "type": "1" 
    "sectype": null
    "asub": "[Optional] The subject of the message displayed inside app (80 Chars)",
    "amsg": "[Optional] The intended message displayed inside app (500 Chars)",
    "acta": "[Optional] The cta link parsed inside the app",
    "aimg": "[Optional] The image url which is shown inside the app",
    "etime": "[Optional] if given, notif will be deleted after this in epoch"
    "hidden" :"[Optional] if given, notif will not show in user feed"
  },
    "recipients": 0x0
}

```
<br>

##### **Subset Payload** :arrow_right:

```
{
  "notification": {
    "title": "The title of your message displayed on screen (50 Chars)",
    "body": "The intended message displayed on screen (180 Chars)"
  },
  "data": {
    "type": "4"
    "sectype": null
    "asub": "[Optional] The subject of the message displayed inside app (80 Chars)",
    "amsg": "[Optional] The intended message displayed inside app (500 Chars)",
    "acta": "[Optional] The cta link parsed inside the app",
    "aimg": "[Optional] The image url which is shown inside the app",
    "etime": "[Optional] if given, notif will be deleted after this in epoch"
    "hidden" :"[Optional] if given, notif will not show in user feed"
  },
  "recipients": [
     0x1: null,
     0x2: null,
     ...
     0xn: null
}

```
<br>

##### **Secret Payload** :arrow_right:

```
{
  "notification": {
    "title": "The title of your message displayed on screen (50 Chars)",
    "body": "The intended message displayed on screen (180 Chars)"
  },
  "data": {
    "type": "4" 
    "sectype": "aes+eip85"
    "asub": "encrypted by secret using sectype | [Optional] The subject of the message displayed inside app (80 Chars)",
    "amsg": "encrypted by secret using sectype | [Optional] The intended message displayed inside app (500 Chars)",
    "acta": "encrypted by secret using sectype | [Optional] The cta link parsed inside the app",
    "aimg": "encrypted by secret using sectype | [Optional] The image url which is shown inside the app",
    "etime": "[Optional] if given, notif will be deleted after this in epoch"
    "hidden" :"[Optional] if given, notif will not show in user feed"
  },
  "recipients": [
     0x1:[{
     secret: [secret used to encrypt]
     }],
     0x2: [{
     secret: [secret used to encrypt]
     }],
     ...
     0xn: [{
     secret: [secret used to encrypt]
     }]
        ]
}

```
<br>

##### **Additional Meta Payload** :arrow_right:

```ts
{
  "data": {
    "acta": "",
    "aimg": "",
    "amsg": "VideoCall",
    "asub": "VideoCall",
    "type": "3",
    "additionalMeta": {
      "type": "1+1", // <type>+<version>
      "data": '{"chatId":"c04c90ba7057c10c59925f36ec7952bd7e7f9436517977115da2bdcd5b28ec30","status":4,"senderAddress":"0x842a882b4c054801F06d52181231A77e467BE41f","signalingData":null,"recipientAddress":"0x459AB94401A00AdD8C6e230596Bde9B2F113E8BE"}',
      "domain": "push.org" // optional
    }
  },
  "recipients": "0x459AB94401A00AdD8C6e230596Bde9B2F113E8BE",
  "notification": {
    "body": "Video Call from 0x842a882b4c054801F06d52181231A77e467BE41f",
    "title": "Video Call from 0x842a882b4c054801F06d52181231A77e467BE41f"
  }
}
```