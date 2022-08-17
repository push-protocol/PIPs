
| title  | description  | author  |  status |  type |  category | subcategory | niche | created |
|---|---|---|---|---|---|---|---|---|
| The PIP title is a few words, not a complete sentence  | Description is one full (short) sentence | The list of the author's name(s) and username(s), or name(s) and email(s).  | Draft / Living / Review / Final  | One of Standards Track, Process, or Informational | (Optional field, only needed for Standards Track PIPs) One of Core, Network, Interface, Storage, or PRC | (Optional field, only needed if proposal is to improve subcategory) | (Optional field, only needed if proposal is to improve a niche of a subcategory) | YYYY-MM-DD Date the PIP was created on (ISO 8601 format) |

This is the suggested template for new PIP. More info about type, category, subcategory, niche can be found in [PIP-1](./PIPs/PIP-1-workflow-index) or in [Definitions & Specs](./definitions). Note that a PIP number will be assigned by an editor. When opening a pull request to submit your PIP, please use an abbreviated title in the filename, `pip-number-title-abbrev.md`.

**The title should be 64 characters or less. It should not repeat the PIP number in title, irrespective of the category.**

Each Proposal should have the following parts:

* **Abstract** - Abstract is a multi-sentence (short paragraph) technical summary. This should be a very terse and human-readable version of the specification section. Someone should be able to read only the abstract to get the gist of what this specification does.

* **Motivation**  - A motivation section is critical for Proposals that want to change or amend the Standards. It should clearly explain why the existing Standard specification is inadequate to address the problem that the proposed solves. Proposals without sufficient motivation may be rejected outright.

* **Specification** - The technical specification should describe the syntax and semantics of any new feature.

* **Rationale** (*optional)- The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternate designs that were considered and related work. The rationale should discuss important objections or concerns raised during discussion around the Proposal.

* **Test Cases** - Test cases for an implementation are mandatory for PIPs that are affecting consensus changes. If the test suite is too large to reasonably be included inline, then consider adding it as one or more files in ../assets/pip-####/.

* **Reference Implementation** (*Optional)- An optional section that contains a reference/example implementation that people can use to assist in understanding or implementing this specification.
