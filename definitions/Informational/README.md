# Types

There are three major categories of PIPs, as well as more specific subcategories:

1. A Standards Track PIP describes any change that affects most or all EPNS implementations, such as—a change to the network protocol, a change in block or transaction validity rules, proposed application standards/conventions, or any change or addition that affects the interoperability of applications using Ethereum. Standards Track EIPs consist of three parts—a design document, an implementation, and (if warranted) an update to the formal specification. Furthermore, Standards Track EIPs can be broken down into the following categories:

    * `Core`: improvements requiring a consensus fork or changes in Push nodes, as well as changes that are not necessarily consensus critical but may be relevant to “core dev” discussions, and the miner/node strategy changes.

    * `Interface` - : includes improvements around client API/RPC specifications and standards, and also certain language-level standards like method names and contract ABIs. The label “interface” aligns with the [interfaces repo] and discussion should primarily occur in that repository before an PIP is submitted to the PIPs repository.

    * `Networking` - includes networking specifications and proposals around how push nodes communicate and interoperate.

    * `PRC` - signifies, application-level standards and conventions, including notification, chat payloads, and content markdown. It also includes subcategories.

        * `Notifications` -  follow composable blocks that help achieve modular structure and help in building on top of them:

        * `Chat` -  \<WIP>

2. A Meta PIP describes a process surrounding EPNS or proposes a change to (or an event in) a process. Process PIPs are like Standards Track PIPs but apply to areas other than the EPNS protocol itself. They may propose an implementation, but not to EPNS codebase; they often require community consensus; unlike Informational PIPs, they are more than recommendations, and users are typically not free to ignore them. Examples include procedures, guidelines, changes to the decision-making process, and changes to the tools or environment used in EPNS development. Any meta-PIP is also considered a Process PIP.

3. An Informational PIP provides general guidelines or information to the EPNS community, but does not propose a new feature. Informational PIPs do not necessarily represent a EPNS community consensus or recommendation, so users and implementors are free to ignore Informational PIPs or follow their advice.

It is highly recommended that a single PIP contain a single key proposal or new idea. The more focused the PIP, the more successful it tends to be. e.g. - A typo or single change in payloads doesn't require PIP. It should be contributing as major improvement or change multiple clients.

A PIP must meet certain minimum criteria. It must be a clear and complete description of the proposed enhancement. The enhancement must represent a net improvement. The proposed implementation, if applicable, must be solid and must not complicate the protocol unduly.
