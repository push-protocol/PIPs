| title  | description  | author  |  status |  type |  category | subcategory | created |
|---|---|---|---|---|---|---|---|
| ENS support in Push Notifications | Sending notifications by specifying reciver's ENS domains rather than Eth Address | Aman Gupta <aman@epns.io> | Draft | Standard | PRC | Notification | 2022-11-21 |

* **Abstract** - Ethereum Name Service (ENS) support should be added while sending Push Notification from DApp / SDK which enables sender channel to specify an ENS domain as reciever rather than providing the Eth Address.

* **Motivation**  - Since ENS domains map human-readable names to machine-readable identifiers such as 'Ethereum Address', it makes sending notifications much easier and seemless without the need of storing, remembering and copy/pasting the long addresses

* **Specification** - While sending a notification a channel should be able to specify either an ethereum address or an ENS Domain as reciver (Note - There can also be multiple ens domains as recivers for a subset notification). The Push Node should be able to resolve these ENS domains send the notifications to the specified address.

* **Rationale** - ENS is the most widely integrated blockchain standard which can help making Push Notifications to be more user friendly and simpler to use by eliminating copying and pasting long addresses. Two approaches were discussed for this feature which mainly differs on resolving ENS domains part. First approach suggests to resolve the domains on DApp / SDK itself and send to Push Nodes as simple address whereas second approach suggests the responsibility of resolving ENS domains should be of Push Nodes to maintain formity as push nodes notifications can have multiple sources (contract / graph etc). The latter approach is choosen due to the above reason.

* **Reference Implementation** -
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
     abc.eth: null,
     bcd.eth: null,
     ...
     xyz.eth: null
}

```