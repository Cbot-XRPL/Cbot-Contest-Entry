## Project Overview 📖

- **Project Name:** URI_Token_Remit.c
- **Folder Project Name Inside submissions Branch:** URI-Token-Remit
- **Project Description:** This hook is designed to automatically distribute URI Tokens (RWA or NFT) based on the Xahau hook rule engine.

## Project Details 🛠

- [X] **Included Project Files (code, documentation, etc.)**
- [X] **Detailed `README.md` file containing:**

  - **Project Description**
This hook is designed to autonomously distribute URI Tokens (RWA or NFT) based on the Xahau hook rule engine. This hook could potentially replace a transfer agent, allowing users a secure way to get assets without a broker. This hook will essentially allow you to register unique assets for distribution at a Xahau address. Some potential assets that could be distributed based on this hook are art, real estate, tickets, and digital products. This hook is complaint with current NFT standard XLS-53 and will work with the upcoming Bidds marketplace. If you want roytlies paid on your sales you will also need Broker || Royalty hook when it become available. You can find an example of this hook on Mainnet at [address] and our Concert Rental Tickets on testnet installed at [address]. These exampkes are going online before Febuary 1st.

  - **Instructions on How to Use the Project**
  The hook is installed on an account. The length of your URIs (in bytes) set through a parameter called URIL. URIs and their NUM can be added or removed from the hook state via invoke transactions. It is crucial that all URIs have the exact same length, as this consistency is key to the hook's functionality (more details on this below). You must also specify the cost to charge users for minting a URI token. This hook includes an optional lock system, allowing a passkey to be set to gate the "HOOK ON" functionality. The primary function of this hook is triggered when a payment is sent to the account where it is installed. Upon activation, the hook checks a ruleset, mints a URI token, and sends it to the payee's account. The URI tokens are minted in the order they are numbered with the NUM param. Upon completion of the URI token mint the assocated URI and NUM key are deleted from hook state.

  - **Integration Details for Xahau Hooks - if used**
This project is a new hook for Xahau. This URI Token Remit hook is essentially the NFT minting contract EVM uses to distribute NFTs but with special features only hooks can provide. This hook has zero depencys and is built to on
The lock feature demonstrates Xahau Hooks' unique ability to gate incoming transactions. It works by allowing the hook owner to set a six-digit passcode. If the passcode is not submitted with the payment as a parameter and the lock has been enabled by the hook owner, the hook will reject the payment. This feature is particularly useful for commercial implementations that require gating asset distribution to qualified investors or buyers.
## How to Use the Project 🚀

### Adding URIs

Its key all your URIs have the same Charater count or the hook will break. Test adding and minting on testnet before using this hook on mainnet. Xahau is very specfic about predicting sizes of data passed around. Its sujested your metadata files for the URIs to be available at one base URI like a folder on IPFS. See the example of how I achived a consitant char count accross URIS.

- ipfs://bafybeieoyz3sghr27ybimhssgahaba5of6anmldjjtmufsxen22gmenjl4/00000**1**.json
- ipfs://bafybeieoyz3sghr27ybimhssgahaba5of6anmldjjtmufsxen22gmenjl4/00000**2**.json
- ipfs://bafybeieoyz3sghr27ybimhssgahaba5of6anmldjjtmufsxen22gmenjl4/00000**3**.json
- ipfs://bafybeieoyz3sghr27ybimhssgahaba5of6anmldjjtmufsxen22gmenjl4/00000**4**.json

### Hook Parmeters
To add and remove state for this hook you will use ```TTINVOKE``` transactions on the account with the parameter you intend to set. You can track your hook state at [XRPLWin Hook Testnet](https://xahau-testnet.xrplwin.com/):

|PARAM|NUMBER|
|-----------|-------|
|**URIL:**|The lenght in bytes of your base URI after it hex / 2. Use the XRPL Hex Visualizer Tool to convert your URIL to a unit64 before use in hook params. This needs to set before adding the base URI. This can be updated as needed. Beware if the URIL is not correct URI lenght your state saves and subsiquent mints will fail. You can catch this by looking at you state with XRPL WIN Hook Tracking Tools and ensure a consitant entry pattern.
|**URI:**|The URI pointer to your metadat. Use the XRPL Hex Visualizer Tool to convert your URI to a hex string before use in hook params. This needs to set at the same time as the NUM param. This can be updated by re-entering the URI with the same NUM key to reset it|
|**NUM:**|The number of your spefic URI metadata for entry. Use the XRPL Hex Visualizer Tool to convert your name/number to unit64 before use in hook params. Name/number your files 000001, 000002, 000003 .. and so on, that way the counter in the hook can file and mint them in order. They can be updated after being added. A small handful of numbers are already allocated for use in this hook functions. Do not use 999999-999991 for URI token NUMs.|
|**COST:**|How Much XAH you want to charge for a URI emisson. Use the XRPL Hex Visualizer Tool to convert your COST number to a unit64 before use in hook params. This needs to set before adding URI number keys. This can be updated as needed.|
|**LOCK:**|A numerical passkey. If this param is set hook users will have to submit the PASS param to unlock and use the hooks fuctionality. Use the XRPL Hex Visualizer to convert your LOCK number to a unit64 before use in hook params. This can be updated as needed.|
**COUNT:**|A optional param to adjsut the hooks counter state. This param does not need to be used in most cases the hook will keep count when adding and removing state. If you reset a certain peice of state or deal with hook errors there is a chance your counter has gone out of sync. Ensure the COUNT param is set to the total number of URIs in your hook state. You can see the counter in the  XRPL WIN Hook Tracking Tools
|**PASS:**|A numerical passkey. If a hook is locked this param must be submited as a param with a payment transaction to unlock it. Use the [XRPL Hex Visualizer](https://transia-rnd.github.io/xrpl-hex-visualizer/) to convert your PASS number to a unit64 before use in hook params.|
|**DEL**| List the number of the hook state you want to delete.|

### Hook State Number Keys
These are the number keys to param data stored in hook state. When debuging and looking at your hook state and namespace you will see these keys holding you data. Your not intented to enter these key number with the exception of the NUM with the URI entry.
|STATE|NUMBER|HEX|
|-----------|-------|------|
|URIL|999999|00000000000F423F|
|URI & NUM|000001-999990| 0000000000000001 - 00000000000F4236|
|COST|999997| 00000000000F423D|
|LOCK|999996| 00000000000F423C|
|COUNT|999995| 00000000000F423B|
|ROY|ROYALTY| 524F59414C5459|

### Hook Install
Detailed hook install information will be available in the README.MD.

## Integration with Xahau Hooks 🔗

This project is a new hook for Xahau. This URI Token Remit hook is essentially the NFT minting contract EVM uses to distribute NFTs but with special features only hooks can provide. This hook has no dependency to function it can live on address and be loaded with invokes. Users can send payments and according to rules it will give them assets. The hook has serveral customizations in a low requirement package to make it functional as possible for testing and eventual commerical use. With the current features it cost 0.004 XAH to fire (with editing much less) but it does not require any other hooks, applications, ect to function. For just a few XAH you can load up and fire off thousands of assets.

## Mandatory Tweets 🐦

Submissions will be shared and amplified by the @XahauNetwork account, giving your work additional visibility within the community.
- [X] **First Mandatory Tweet** announcing your participation:

  - **Link to Tweet:** [https://x.com/Cbot_Xrpl/status/1878540427587907898]

- [ ] **Second Mandatory Tweet** upon submission for final review:

  - **Link to Tweet:** [Insert the link to your submission tweet here]

  **Example Tweet:**
  > We have submitted [Project Name] to the Build on Xahau contest, see our submission here: [PR Link]

## Additional Information 📄

Any additional information, notes, or comments you want to include with your submission.
