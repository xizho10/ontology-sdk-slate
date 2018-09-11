---
title: Ontology dAPI Reference

language_tabs: # must be one of 
  - typescript

toc_footers:
  - <a href='https://github.com/ontio/ontology-dapi'>ontology-dapi</a>
  - <a href='https://github.com/ontio/ontology-dapi-demo'>ontology-dapi-demo</a>
  - <a href='https://ont.io'>Powered by Ontology</a>

includes:
 

search: false
---

# Abstract

This proposal has two major parts:

* A Javascript API is proposed for dApps development. This dAPI allows dApps to communicate with Ontology blockchain and make requests for transfers, ONT ID registration and others, without requiring users to trust the dApp itself. The issue of trust is shifted to the dAPI provider.

* A Communication protocol is proposed for dAPI provider development. This allows multiple Wallet implementators to offer the same unified service to users of dApps and prevent fragmentation of dApp development.

# Motivation

Currently a dApp will use one of the SDKs (Typescript, Java, Python, ...) to communicate with Ontology network. This setup has three main disadvantages:

1. User of the dApp will have to trust the dApp developer with his private keys and that information about transfers mediated through the dApp are legitimate.

2. Although the SDKs are very powerful, they are hard to use. A more streamlined API will allow developers to focus on the application itself.

3. Hard to implement integration to external signing mechanism (e.g.: Ledger, Trezor)

# Specification

This proposal makes use of the following functions and definitions:

* **SDK**, a software development kit implementing low level communication with the network and providing high level interface for dApps.

* **dApp**, an application with decentralised characteristics running in web environment. The application uses Ontology network for value transfers, contracts enforcing and identification between participants.

* **dAPI**, the API for dApps this OEP is proposing.

* **dAPI provider**, an implementation of the dAPI in the form of web browser plugin or other means, where a user interaction with the provider can be injected into api call workflow (e.g.: confirming transfer).

* **Notify event**, an event broadcasted from smart contract execution.

* **NEOVM**, a lightweight virtual machine for execution of Neo/Ontology smart contracts.

## Asynchronicity and error handling

All the functions except ```Utils``` component are communicating with extension through asynchronious message channel. Therefore all the methods are returning Promises. 

The promises will be either resolved immediately if no interaction with user UI or blockchain is required or later when the user action takes place/blockchain responds. In case the call to method trigger an error, the error code is transmitted in rejected promise. Specific error codes are described with every method.

## Account/Identity management

Because dAPI shifts the issue of trust from dApp to dApp provider, all account and identity management is external to the dApp. Therefore there are no methods which directly handle private keys. The dApp won't need to sign the transaction itself. 

Any time dApp makes a call that requires a private key to sign something (makeTransfer, sign), dApp provider will inform user about the action and prompt him for permission.

dApp provider can even forward the request to external signing mechanism as part of the process. This way the dApp does not need to specifically integrate with such mechanism.

dAPI providers can choose to support multiple accounts and identities. Account and identity switching is part of dAPI provider implementation. dAPI provider should share with dApp as little information about user accounts and identities as possible, because it posses a security risk. Otherwise malicious dApp can list all user accounts with balances and identities.

### dAPI access restriction

Using dAPI any dApp is able to call the dAPI provider and initiate an interaction with the user (e.g.: <code>makeTransfer</code>). Only prerequisite is, that the user visits the dApp page. Although the user will need to confirm such an action, bothering him with this action, if he has no intention to confirm it, will hinder the experience.

Therefore the dAPI will forward with every request the <code>Caller</code> object containing the <code>url</code> of the dApp page or <code>id</code> of another extension trying to communicate with dAPI provider. It is upto the dAPI provider to implement custom permission granting workflow or automatic blacklisting.

```typescript

interface Caller {
  url?: string;
  id?: string;
}
```
## Encoding

The interaction with dAPI often requires specification of ```Address```, ```Identity```, ```Contract address``` or ```Public Key```. Those concepts are represented by string representation with specific encodings.

### Address

* 34 bytes long
* using Base58 check encoding
* starts with A letter

### Contract address

* 40 bytes long
* using Hex encoding

### Identity

* 42 bytes long
* using Base58 check encoding for 34 byte suffix
* starts with 'did:ont:' prefix

### Public Key

* 33/35 bytes long
* using Hex encoding


## Complex structures

All the functions of this dAPI, which requires arguments are using one typed argument instead of many. The reasons are better readability and future extensibility. 

API specification is a complex document. Every method has some inputs and outputs. Although we use the primitive types (numbers, strings, booleans) whenever possible, there are places where a complex object is required. To precisely describe the structure of those objects, we'd chosen Typescript-like syntax.


## Components

Although this proposal is bringing clear and simple API for the dApps, the individual functions can be divided into these components:

* **Network**, a thin wrapper around the Ontology Node API, masking the complexity of rpc/rest calls and web-sockets with Request-Response facade.

* **Provider**, functions for getting information about dAPI provider

* **Asset**, functions for transferring assets between user account and others.

* **Identity**, functions for interacting with own ONT-ID identity.

* **SmartContract**, a high level wrapper around the Smart Contract invocation and deployment.

* **Message**, functions for signing arbitrary messages.

* **Utils**, a group of utility function for encoding and decoding the data from/to blockchain.


# Components

## Network

A network API consists of:

```typescript

type NetworkType = 'MAIN' | 'TEST' | 'PRIVATE';
type Asset = 'ONT' | 'ONG';

interface Network {
  type: NetworkType;
  address: string;
}

function getGenerateBlockTime(): Promise<number | null>
function getNodeCount(): Promise<number>
function getBlockHeight(): Promise<number>
function getMerkleProof({ txHash: string }): Promise<MerkleProof>
function getStorage({ contract: string, key: string }): Promise<string>
function getAllowance({ asset: Asset, fromAddress: string, toAddress: string }): Promise<number>
function getBlock({ block: number | string }): Promise<Block>
function getTransaction({ txHash: string }): Promise<Transaction>
function getNetwork(): Network
function getBalance({ address: string }): Promise<Balance>

```

For further explanation about the wrapped method consult https://ontio.github.io/documentation/restful_api_en.html . The types **Transaction**, **Block**, **MerkleProof** and **Balance** corresponds to the exact object returned from Ontology blockchain.

TODO: copy the definition of all network api calls with inputs and outputs from ontology documentation.


## Provider

A primary focus of Provider API is to check if user has installed any dAPI provider and to get information about it.

### getProvider


```typescript

interface Provider {
  name: string;
  version: string;
  compatibility: string[];
}

function getProvider(): Promise<Provider>

```


Returns the information about installed dAPI provider if there is one installed. <code>compatibility</code> refers to all OEPs this dAPI provider supports. E.g.:

```typescript

compatability: [
    'OEP-6',
    'OEP-10',
    'OEP-29'
]

```

dAPI provider does not need to support all future OEPs concerned with dAPI.

* Rejects with **NO_PROVIDER** in case there is no dAPI provider installed.

## Asset

A primary focus of Asset API is to initiate a transfer. The request needs to be confirmed by the user.

### getAccount

```typescript

function getAccount(): Promise<string>	

```
Returns currently selected account of logged in user. 	
 * Rejects with ```NO_ACCOUNT``` in case the user is not signed in or has no accounts

### makeTransfer

```typescript
function makeTransfer({ recipient: string, asset: Asset, amount: number }): Promise<string>
```

Initiates a transfer of <code>amount asset</code> to <code>recipient</code> account. 

The amount should always be an integer value. Therefore is is represented in the smallest, further non divisible units for the asset. E.g.: If the <code>asset</code> is ONG then the value is multiplied by 1000000000.

Returns transaction Id.

* Rejects with ```NO_ACCOUNT``` in case the user is not signed in or has no accounts
* Rejects with ```MALFORMED_ACCOUNT``` in case the <code>recipient</code> is not a valid account
* Rejects with ```CANCELED``` in case the user cancels the request

## Identity

A primary focus of Identity API is to interact with ONT ID smart contract on the blockchain.

### getIdentity


```typescript
function getIdentity(): Promise<string>	
```

 Returns currently selected identity of logged in user.	
 * Rejects with ```NO_IDENTITY``` in case the user is not signed in or has no identity


### getDDO
```typescript
interface OntIdDDO {
    ...
}

function getDDO({ identity: string }): Promise<OntIdDDO>
```

Queries Description Object of the <code>identity</code>. This call must query the blockchain. This operation is not signed and therefore does not require user interaction.

Returns Description object of the <code>identity</code>. This object contains public keys and attributes of the identity.

* Rejects with ```MALFORMED_IDENTITY``` in case the <code>identity</code> is not a valid identity

### addAttributes

```typescript
function addAttributes({ attributes: OntIdAttribute[] }): Promise<void>
```

Initiates adding of attributes to the user identity. This action needs to be confirmed by the user. Attributes with existing <code>key</code> will be overwritten.

* Rejects with ```NO_IDENTITY``` in case the user is not signed in or has no identity

### removeAttribute
```typescript
function removeAttribute({ key: string }): Promise<void>
```

Initiates removing of attribute from the user identity. This action needs to be confirmed by the user.

* Rejects with ```NO_IDENTITY``` in case the user is not signed in or has no identity


## Message
This API deals with arbitrary message signing and verification.

### signMessageHash
```typescript

interface Signature {
  publicKey: string;
  data: string;
}

function signMessageHash({ messageHash: string }): Promise<Signature>
```

Initiates signing of arbitrary <code>messageHash</code> by the user account or identity. dAPI provider should provide the user with a way for selecting which account or identity will sign the message.

Returns the <code>Signature</code> object containing both the <code>publicKey</code> and signature <code>data</code> needed for signature validation.

This method does not require the dApp to disclose the message itself, only the hash. 

Because malicious dApp can hash a real prepared transfer transaction and plant it for signing, that posses a risk to the user.
Therefore the hash is prepended with known string ```Ontology message:```, and only this hash is put for signing.

* Rejects with ```NO_ADDRESS``` in case the user is not signed in or has no account or identity
* Rejects with ```MALFORMED_MESSAGE``` in case the <code>message</code> is not hex encoded

### verifyMessageHash
```typescript
function verifyMessageHash({ messageHash: string, signature: Signature }): Promise<boolean>
```

Verifies that the <code>signature</code> is valid signature of <code>messageHash</code>. 

This method does not require the dApp to disclose the message itself, only the hash. The hash is prepended with known string ```Ontology message:``` and only this hash is put for verification.

* Rejects with ```MALFORMED_MESSAGE``` in case the <code>message</code> is not hex encoded
* Rejects with ```MALFORMED_SIGNATURE``` in case the <code>signature</code> is not in valid format

### signMessage
```typescript
function signMessage({ message: string }): Promise<Signature>
```

Initiates signing of arbitrary <code>message</code> by the user account or identity. dAPI provider should provide the user with a way for selecting which account or identity will sign the message.

Returns the <code>Signature</code> object containing both the <code>publicKey</code> and signature <code>data</code> needed for signature validation.

This method provide the dAPI provider with the message body, which it should display to the user prior to signing (e.g.: a contract to sign).

* Rejects with ```NO_ADDRESS``` in case the user is not signed in or has no account or identity

### verifyMessage
```typescript
function verifyMessage({ message: string, signature: Signature }): Promise<boolean>
```

Verifies that the <code>signature</code> is valid signature of <code>message</code>. 

* Rejects with ```MALFORMED_MESSAGE``` in case the <code>message</code> is not hex encoded
* Rejects with ```MALFORMED_SIGNATURE``` in case the <code>signature</code> is not in valid format


## SmartContract
The main functionality of this component is invocation of smart contract methods.

### invoke
```typescript
type ParameterType = 'Boolean' | 'Integer' | 'ByteArray' | 'Struct' | 'Map' | 'String';

interface Parameter {
    type: ParameterType;
    value: any;
}

type Result = string[];

interface Response {
    transaction: string;
    results: Result[];
}

function invoke({ contract: string, method: string, parameters?: Parameter[], 
  gasPrice?: number, gasLimit?: number, requireIdentity?: boolean }): Promise<Response>
```

Initiates a <code>method</code> call to a smart <code>contract</code> with supplied <code>parameters</code>.
The <code>gasPrice</code> and <code>gasLimit</code> are hints for the dAPI provider and it should allow user to override those values before signing. It is upto the dAPI provide to allow user select the payer's account.

In case the smart contract requires the call to be signed also by an identity, parameter <code>requireIdentity</code> should be set to true.

Smart code execution is two step process:

* The transaction is send to the network.
* The transaction is processed and recorded to the blockchain at a later time.

The <code>invoke</code> function will finish only after the transaction is processed by the network. 

Returns <code>transaction</code> hash and array of <code>results</code>.

To output a result from smart contract, call Runtime.Notify method. For every such a call, one result will be outputed.

* Rejects with ```NO_ACCOUNT``` in case the user is not signed in or has no accounts
* Rejects with ```MALFORMED_CONTRACT``` in case the <code>contract</code> is not hex encoded contract address

### invokeRead
```typescript
function invokeRead({ contract: string, method: string, parameters?: Parameter[] }): Promise<any>
```

Initiates a <code>method</code> call to a smart <code>contract</code> with supplied <code>parameters</code> in read only mode (preExec). This kind of method call does not write anything to blockchain and therefore does not need to be signed or paid for. It is processed without user interaction.

Returns direct value returned by the smart contract execution. 

* Rejects with ```MALFORMED_CONTRACT``` in case the <code>contract</code> is not hex encoded contract address


### deploy
```typescript
function deploy({ code: string, name?: string, version?: string, author?: string, 
    email?: string, description?: string, needStorage?: boolean, gasPrice?: number, gasLimit?: number }): Promise<any>
```

Initiates deployment of smart contract. The <code>code</code> parameter represents compiled code of smart contract for NEOVM. The <code>gasPrice</code> and <code>gasLimit</code> are hints for the dAPI provider and it should allow user to override those values before signing. It is upto the dAPI provide to allow user select the payer's account.

* Rejects with ```NO_ACCOUNT``` in case the user is not signed in or has no accounts




# Repo

## ontology-dapi

Green colored components represent ```dAPI.js```. It is universal implementation of communication channel for direct use by dApp developers in web browsers.

https://github.com/OntologyCommunityDevelopers/ontology-dapi

## dAPI provider

Blue colored components belong to specific implementation of dAPI provider. The implementation is out of scope of this proposal, but the implementator must adhere to the protocol used by dAPI.js.

https://github.com/OntologyCommunityDevelopers/ontology-plugin-wallet


## Communication protocol
The communication protocol has RPC style of communication. The RPC is modeled on top of standard WebExtension message passing using <code>runtime.sendMessage</code> and <code>runtime.onMessage.addListener</code>. All the complications of WebExtension is hidden for both the ```dApp```' and ```dAPI provider``` when using dAPI.js.

dAPI providers might use dAPI.js as the communication protocol, but they can also implement different protocols suitable for the specific environment (e.g: iOS, Android, Desktop).

## Architecture
The interaction between dApp and Ontology network can be described with this diagram:
https://github.com/backslash47/OEPs/blob/oep-dapp-api/OEP-6/OEP-6-1.svg

![image](https://github.com/backslash47/OEPs/blob/oep-dapp-api/OEP-6/OEP-6-1.svg)
