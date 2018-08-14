# Key

Class Key is the super class of PublicKey and PrivateKey.

```typescript
class Key {
    algorithm: KeyType;
    parameters: KeyParameters;
    key: string;
    
    constructor(key: string, algorithm?: KeyType, parameters?: KeyParameters)

    computeHash(msg: string, scheme: SignatureScheme): string
    isSchemaSupported(schema: SignatureScheme): boolean
    serializeJson(): JsonKey
}
```
> We usually do not use Key directly, we use PrivateKey and PublicKey instead.

```typescript
import {Crypto} from 'ontology-ts-sdk';
const privateKey = new Crypto.PrivateKey('xxxxxxxx......');

```

### Attributes

```algorithm``` implies the key pair generation algorithm, value is the instance of [KeyType](#keytype). Ontology now supports three kinds of algorithms:

- ECDSA
- SM2
- EDDSA

ECDSA is the default one.

```parameters``` implies the [elliptic curve](#keyparameters) of key's algorithm.

```key``` is the value of key.

## computeHash
Computes hash of message using hashing function of signature schema.

### Parameters
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| msg      |   string   |  Hex encoded input data           |
| scheme   | [SignatureScheme](#signaturescheme) | Signing scheme to use |


### Return Value	
string.


## isSchemaSupported
Tests if signing scheme is compatible with key type.

### Parameters
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| schema    | [SignatureScheme](#signaturescheme) | Signing scheme to use |

### Return Value
boolean

## serializeJson
```typescript
import { Crypto } from 'ontology-ts-sdk';
const private = Crypto.PrivateKey.random();
const jsonKey = private.serializeJson();
console.log(jsonKey);
```
> The result is:

```
{ algorithm: 'ECDSA',
  parameters: { curve: 'P-256' },
  key: 'af0a1903e0ed2774311eec14abb30b5ea0bc6bcfb02f2cb0c4f38b7b5af9a52e' }
```

```typescript
/**
 * Json representation of the Key.
 */
interface JsonKey {
	algorithm: string;
    parameters: JsonKeyParameters;
    key: string | null;
    external?: any | null;
}

/**
 * Json representation of the Key parameters.
 */
export interface JsonKeyParameters {
    curve: string;
}
```

Gets JSON representation of the key(Public/Private key).

### Return Value
JsonKey



# KeyType

```typescript
class KeyType {
    label: string;
    hex: number;
    defaultSchema: SignatureScheme;
    
    constructor(label: string, hex: number, defaultSchema: SignatureScheme)
    
    static ECDSA = new KeyType('ECDSA', 0x12, SignatureScheme.ECDSAwithSHA256);
	static SM2 = new KeyType('SM2', 0x13, SignatureScheme.SM2withSM3);
	static EDDSA = new KeyType('EDDSA', 0x14, SignatureScheme.EDDSAwithSHA512);
	
	static fromHex(hex: number): KeyType
	static fromLabel(label: string): KeyType
	
}
```
> how to use

```typescript
 import {Crypto} from 'ontology-ts-sdk';
 const curve = Crypto.KeyType.ECDSA;
```

### Attributes

```label``` is the name of the key type.

```hex``` is the hex string format of the key type.

```defaultSchema``` is the default [SignatureScheme](#signaturescheme) the key uses.

## fromHex
```typescript
import { Crypto } from 'ontology-ts-sdk';
const keyType = Crypto.KeyType.fromHex(0x12);
//keyType is ECDSA now
	
```

Finds Key type corresponding to specified hex representation.

### Parameters
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| hex   | number | Byte hex value  |


### Return Value
KeyType. If no matched key type, an Error will be thrown.

## fromLabel
```typescript
import { Crypto } from 'ontology-ts-sdk';
const keyType = Crypto.KeyType.fromLabel('SM2');
```
Finds Key type corresponding to specified label representation.

### Parameters
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| label | string | the label of the KeyType  |

### Return Value
KeyType. If no matched key type, an Error will be thrown.

# KeyParameters

```typescript
class KeyParameters {
	curve: CurveLabel
	static deserializeJson(json: JsonKeyParameters): KeyParameters
	constructor(curve: CurveLabel)
	serializeJson(): JsonKeyParameters
}
```

### Attributes
```curve``` implies the [curve label](#curvelabel).

## deserializeJson
```typescript
import { Crypto } from 'ontology-ts-sdk';
const json = {
	curve: 'P-256'
}
const KeyParameters = Crypto.deserializeJson(json);

```

### Parameters
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| json | JSON | JSON representation of KeyParameters |

### Return Value
KeyParameters

## serializeJson
```typescript
import { Crypto } from 'ontology-ts-sdk';
const json = {
	curve: 'P-256'
}
const keyParameters = Crypto.deserializeJson(json);
const json2 = keyParameters.serializeJson();

```

# CurveLabel

```typescript
class CurveLabel {
	label: string;
	hex: number;
	preset: string;
	
	constructor(label: string, hex: number, preset: string)
	
	static SECP224R1 = new CurveLabel('P-224', 1, 'p224');
    static SECP256R1 = new CurveLabel('P-256', 2, 'p256');
    static SECP384R1 = new CurveLabel('P-384', 3, 'p384');
    static SECP521R1 = new CurveLabel('P-521', 4, 'p521');
    static SM2P256V1 = new CurveLabel('sm2p256v1', 20, 'sm2p256v1');
    static ED25519 = new CurveLabel('ed25519', 25, 'ed25519');
    
    static fromHex(hex: number): CurveLabel
    static fromLabel(label: string): CurveLabel
    
}

```
> how to use

```typescript
 import {Crypto} from 'ontology-ts-sdk';
 const curve = Crypto.CurveLabel.SECP256R1;
```

### Attributes
```label``` is the name of the curve label.

```hex``` is the hex string format of the curve label.

```preset``` is the preset value for display.

## fromHex
```typescript
import {Crypto} from 'ontology-ts-sdk';
const curve = Crypto.CurveLabel.fromHex(2)
```
Finds Curve corresponding to specified hex representation.

### Parameters
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| hex | number | Byte hex value |

### Return Value
CurveLabel

## fromLabel
```typescript
import {Crypto} from 'ontology-ts-sdk';
const curve = Crypto.CurveLabel.fromHex('P-226');
```
Finds Curve corresponding to specified label representation.

### Parameters
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| label | string | The label of the CurveLabel |

### Return Value
CurveLabel


# SignatureScheme
```typescript
class SignatureScheme {
	label: string;
	hex: number;
	labelJWS: string;
	
	constructor(label: string, hex: number, labelJWS: string)
	
	static ECDSAwithSHA224 = new SignatureScheme('SHA224withECDSA', 0, 'ES224');
    static ECDSAwithSHA256 = new SignatureScheme('SHA256withECDSA', 1, 'ES256');
    static ECDSAwithSHA384 = new SignatureScheme('SHA384withECDSA', 2, 'ES384');
    static ECDSAwithSHA512 = new SignatureScheme('SHA512withECDSA', 3, 'ES512');
    static ECDSAwithSHA3_224 = new SignatureScheme('SHA3-224withECDSA', 4, 'ES3-224');
    static ECDSAwithSHA3_256 = new SignatureScheme('SHA3-256withECDSA', 5, 'ES3-256');
    static ECDSAwithSHA3_384 = new SignatureScheme('SHA3-384withECDSA', 6, 'ES3-384');
    static ECDSAwithSHA3_512 = new SignatureScheme('SHA3-512withECDSA', 7, 'ES3-512');
    static ECDSAwithRIPEMD160 = new SignatureScheme('RIPEMD160withECDSA', 8, 'ER160');
    static SM2withSM3 = new SignatureScheme('SM3withSM2', 9, 'SM');
    static EDDSAwithSHA512 = new SignatureScheme('SHA512withEdDSA', 10, 'EDS512');
    
    static fromHex(hex: number): SignatureScheme
    static fromLabel(label: string): SignatureScheme
    static fromLabelJWS(label: string): SignatureScheme
}
```
```
> how to use

```typescript
 import {Crypto} from 'ontology-ts-sdk';
 const scheme = Crypto.SignatureScheme.ECDSAwithSHA256;
```

### Attributes
```label``` is the name of the signature scheme.

```hex``` is the hex format of the signature scheme.

```labelJWS``` is the label in JWS representation.

## fromHex
```typescript
 import {Crypto} from 'ontology-ts-sdk';
 const sheme = Crypto.SignatureScheme.fromHex(1);

```
Finds Signature schema corresponding to specified hex representation.

### Parameters
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| hex | number | Byte hex value |

### Return value
SignatureScheme

## fromLabel
```typescript
 import {Crypto} from 'ontology-ts-sdk';
 const sheme = Crypto.SignatureScheme.fromLabel('SHA256withECDSA');

```
Finds Signature schema corresponding to specified label representation.

### Parameters
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| label | string |  Label of the signature scheme |

### Return value
SignatureScheme

## fromLabelJWS
```typescript
 import {Crypto} from 'ontology-ts-sdk';
 const sheme = Crypto.SignatureScheme.fromLabelJWS('ES256');

```
Finds Signature schema corresponding to specified label representation.

### Parameters
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| label | string | JWS label |

### Return value
SignatureScheme


# PrivateKey
```typescript
class PrivateKey extends Key {
	static random(keyType?: KeyType, parameters?: KeyParameters): PrivateKey
	static deserializeWIF(wifkey: string): PrivateKey
	static generateFromMnemonic(mnemonic: string, derivePath: string = ONT_BIP44_PATH): PrivateKey
	
	sign(msg: string, schema?: SignatureScheme, publicKeyId?: string): Signature
	async signAsync(msg: string, schema?: SignatureScheme, publicKeyId?: string): Promise<Signature>
	getPublicKey(): PublicKey
	decrypt(keyphrase: string, address: Address, salt: string, params?: ScryptParams): PrivateKey
	encrypt(keyphrase: string, address: Address, salt: string, params?: ScryptParams): PrivateKey
	serializeWIF(): string
	
}
```
Class PrivateKey is to manage the private keys, include the encrypted private key. It offers some userful functions.

## random
```typescript
import { Crypto } from 'ontology-ts-sdk';
const privateKey = Crypto.PrivateKey.random();

```
Generates random Private key using supplied Key type and parameters.

### Parameters
| Parameter | Type | Description |
| --------- | ---- | ----------- |
| keyType | [KeyType](#keytype) | Optional value. KeyType.ECDSA is default value|
| parameters | [KeyParameters](#keyparameters) | Optional value. P256 is default |


### Return Value
PrivateKey


## deserializeWIF
```typescript
import { Crypto } from 'ontology-ts-sdk';
const privateKey = Crypto.PrivateKey.deserializeWIF('L5ND28NenjTkexbqNQKUveaQ8ojnVEb3gBFT6R4SRp5icBi6hhsh')
```
Creates PrivateKey from Wallet Import Format (WIF) representation.

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
| wif | string | Private key in WIF format |

### Return Value
PrivateKey

## generateFromMnemonic
```typescript
import { Crypto } from 'ontology-ts-sdk';
const mnemonic = 'doll remember harbor resource desert curious fatigue nature arrest fix nation rhythm';
const privateKey = Crypto.PrivateKey.generateFromMnemonic(mnemonic);
```
Creates PrivateKey from mnemonic according to BIP39 protocol.

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
| mnemonic | string | space separated list of words |
| derivePath | string | Derive path for BIP44. Optional value.Default value is "m/44'/1024'/0'/0/0"|

### Return Value
PrivateKey

## sign
```typescript
import { Crypto, utils } from 'ontology-ts-sdk';
const private = Crypto.PrivateKey.random();
const msg = 'test';
const encoded = utils.str2hexstr(msg);
const signature = private.sign(encoded, Crypto.SignatureScheme.SM2withSM3);

```









