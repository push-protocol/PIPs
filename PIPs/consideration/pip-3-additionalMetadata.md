# Additional Metadata PIP

| title | description | author | status | type | category | subcategory | created |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Inclusion of additionalMeta to the payload | The additionalMeta parameter will extend current notification payload to carry additional data to provide personalized and contextually relevant content. | Ashis Kumar Pradhan (ashis@push.org) | Draft | Standard | PRC | Notification | 2023-05-22 |
- **Abstract** - The plan is to add a new parameter that can carry contextual metadata to the existing notification payload. Any type of data that can be used to supplement the targeted users' notifications may be contained in it.
- **Motivation** - The notifications will be able to convey more contextual metadata in addition to media and CTAs. Anything from sending videocall metadata to opening functionality to reply to chat messages directly from your notification is possible.
- **Specification** - The parameter would have three parameters: `type`, `data`, and an optional parameter `domain`. The structure of it would be:
`{type: string, data: string, domain?: string}`
 The `type` parameter would include uniform data identifying the kind of data present. The actual metadata we are passing would be in the `data` parameter. The `domain`, a final optional parameter, would include details about the entity for which the `additionalMetadata` was defined.
- **Rationale** - At this time, notification can be expanded to piggyback metadata that can carry additional data in addition to the current payload data. In order to increase user engagement and satisfaction, this will have the freedom to transmit pertinent and personalized information to users. Users, on the other hand, will profit from richer and more interactive experiences as a result of applications using the metadata field to provide personalized and contextually relevant content.

**Reference Implementation**

```jsx
{
  "data": {
    "acta": "",
    "aimg": "",
    "amsg": "VideoCall",
    "asub": "VideoCall",
    "type": "3",
    "additionalMeta": {
      "type": "0+1", // <type>+<version>
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