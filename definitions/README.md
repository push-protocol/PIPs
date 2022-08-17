# Definitions about Types, Category, Subcategory and Niche of PIPs

The folder contains specific information about individual Types, Categories, Subcategories and Niche of Push Protocol along with current specs derived from finalized PIPs. Definitions of these topics and things inside them will keep on changing as PIPs are finalized. If you are looking to submit a PIP, please [head over here](../PIPs).

## Understanding PIP Types, Categories, Subcategories and Niche

PIP proposals are classified into **type** which can then optionally be categorized into **category** -> **subcategory** -> **niche**. Type describes the high level standard which the PIP wants to address. Category describes the type drilldown which a specific PIP is created to address. Subcategory dives deeper into a particular category while niche describes the low level component of that subcategory.

### Type

Type decribes the high level standard which the PIP wants to improve.

1. **Standard**  PIP describes any change that affects most or all Push protocol implementations, such as changes in core, interface, networking or application level standards.

2. **Meta** PIP describes a process surrounding Push or proposes a change to (or an event in) a process. Process PIPs are like Standards Track PIPs but apply to areas other than the Push protocol itself. Examples include procedures, guidelines, changes to the decision-making process, and changes to the tools or environment used in Push development. Any meta-PIP is also considered a Process PIP.

3. **Informational** PIP provides general guidelines or information to the EPNS community, but does not propose a new feature. Informational PIPs do not necessarily represent a EPNS community consensus or recommendation, so users and implementors are free to ignore Informational PIPs or follow their advice.

### Category

Categories are only required for **Standard** Type PIPs and define the branch of PUSH Protocol which it targets to improve.

1. **Core**: includes improvements for changes in the network including incentives and rewards, syncing, consensus mechanism changes and processes that might require fork cause of breaking changes.

2. **Interface**: includes improvements around client API/RPC specifications and standards, and also certain language-level standards that may help in standardizing interfacing.

3. **Networking**: includes networking specifications and proposals around how push nodes communicate and interoperate.

4. **PRC**: Signifies, application-level standards and conventions, including verification, identity, payloads, content markdown for notifications, chats or any communication standard that is added.

### Subcategory

Subcategory are optional and mainly required for **PRC** category, they define the particular topic within the Category.

1. **Notification**: Available under Standard > PRC > Notification which addresses specs, proposals and improvements for everything related to push notification protocol.

2. **Chat**: Available under Standard > PRC > Chat which addresses spec, proposals and improvements for everything related to push chat protocol.

### Niche

Niche are optional and are required in some **Subcateory** sections. they define the specific low level funcationality that needs to be changed, improved or addressed.

For Subcategory: **Nofification**

1. **Verification**: Addresses different types of verifications that can be used while sending a notification to Push node.'

2. **Identity**: Identitifies from where a notification payload is coming along with what is the storage mode, protocol to transform it to json payload, etc. 

3. **payload**: Addresses what payload of the notification should contain including the way notification should be encrypted, things payload can carry and how they transform and the recipients for which it is intended to be.

4. **content**: Defines how content inside the notfication can be displayed, mostly markdown for title and the body of notification.

For Subcategory: **Chat**

{TBD}
