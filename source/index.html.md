---
title: Ontology Smart Contract API Reference

language_tabs: # must be one of 
  - python

toc_footers:
  - <a href='https://github.com/ontio/ontology-python-sdk/tree/master/test'>Check for more examples</a>
  - <a href='https://ont.io'>Powered by Ontology</a>

includes:
 

search: false
---

# Introduction

This is a comprehensive Java library for the Ontology blockchain,which is released by Ontology currently supports multiple functions, including native wallet management, digital identity management, digital asset management, smart contract deployment and invocation, node communication, with more to come in the future.

The Ontology official Python SDK is a comprehensive SDK which is based on Python3.x. Currently, it supports local wallet management, digital identity management, digital asset management, deployment and envoke for smart contract, and communication with the Ontology blockchain. The future will also support more functions and applications.

# Network

## network.get_version

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
version = sdk.rpc.get_version()
```

This interface is used to get the version information of the connected node in current network.

### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

### Return Value

| Type  | Description                                   |
| :---: | :-------------------------------------------: |
| str   | the version information of the connected node |

## network.get_node_count

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
count = sdk.rpc.get_node_count()
```

This interface is used to get the current number of connections for the node in current network.

### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

### Return Value

| Type  | Description               |
| :---: | :-----------------------: |
| int   | the number of connections |

## network.get_gas_price

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
price = sdk.rpc.get_gas_price()
```

This interface is used to get the gas price in current network.

### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

### Return Value

| Type  | Description            |
| :---: | :--------------------: |
| int   | the value of gas price |

## network.get_network_id

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
network_id = sdk.rpc.get_network_id()
```

This interface is used to get the network id of current network.

### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

### Return Value

| Type  | Description                       |
| :---: | :-------------------------------: |
| int   | the network id of current network |

## network.get_block_by_hash

```python
from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
block_hash = "44425ae42a394ec0c5f3e41d757ffafa790b53f7301147a291ab9b60a956394c"
block = sdk.rpc.get_block_by_hash(block_hash)
```

This interface is used to get the block information by hexadecimal block hash value in current network.

### Parameters

| Parameter  | Type  | Description                       |
| :--------: | :---: | :-------------------------------: |
| block_hash | str   | a hexadecimal value of block hash |

### Return Value

| Type  | Description                                       |
| :---: | :-----------------------------------------------: |
| dict  | the block information of the specified block hash |

## network.get_block_by_height

```python
from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
height = 0
block = sdk.rpc.get_block_by_height(height)
```

This interface is used to get the block information by block height in current network.

### Parameters

| Parameter | Type  | Description                  |
| :-------: | :---: | :--------------------------: |
| height    | int   | a decimal block height value |

### Return Value

| Type  | Description                                         |
| :---: | :-------------------------------------------------: |
| dict  | the block information of the specified block height |

## network.get_block_count

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
count = sdk.rpc.get_block_count()
```

This interface is used to get the decimal block number in current network.

### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

### Return Value

| Type  | Description                                           |
| :---: | :---------------------------------------------------: |
| int   | the decimal total number of blocks in current network |

## network.get_current_block_hash

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
current_block_hash = sdk.rpc.get_current_block_hash()
```

This interface is used to get the hexadecimal hash value of the highest block in current network.

### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

### Return Value

| Type  | Description                                                        |
| :---: | :----------------------------------------------------------------: |
| dict  | the hexadecimal hash value of the highest block in current network |

## network.get_block_hash_by_height

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
height = 0
block_hash = sdk.rpc.get_block_hash_by_height(height)
```

This interface is used to get the hexadecimal hash value of specified block height in current network.

### Parameters

| Parameter | Type  | Description                  |
| :-------: | :---: | :--------------------------: |
| height    | int   | a decimal block height value |

### Return Value

| Type  | Description                                              |
| :---: | :------------------------------------------------------: |
| str   | the hexadecimal hash value of the specified block height |

## network.get_balance()

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
base58_address = "ANH5bHrrt111XwNEnuPZj6u95Dd6u7G4D6"
address_balance = sdk.rpc.get_balance(base58_address)
ont_balance = address_balance['ont']
ong_balance = address_balance['ong']
```

This interface is used to get the account balance of specified base58 encoded address in current network.

### Parameters

| Parameter      | Type  | Description                      |
| :------------: | :---: | :------------------------------: |
| base58_address | str   | a base58 encoded account address |

### Return Value

| Type  | Description                                     |
| :---: | :---------------------------------------------: |
| dict  | the value of account balance in dictionary form |

## network.get_allowance

```python
from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
base58_address = "AKDFapcoUhewN9Kaj6XhHusurfHzUiZqUA"
allowance = sdk.rpc.get_allowance(base58_address)
```

This interface is used to get the the allowance from transfer-from accout to transfer-to account in current network.

### Parameters

| Parameter      | Type  | Description                      |
| :------------: | :---: | :------------------------------: |
| base58_address | str   | a base58 encoded account address |

### Return Value

| Type  | Description                                                             |
| :---: | :---------------------------------------------------------------------: |
| str   | the decimal allowance from transfer-from account to transfer-to account |

## network.get_storage

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
contract_address = "0100000000000000000000000000000000000000"
key = "746f74616c537570706c79"
value = sdk.rpc.get_storage(contract_address, key)
```

This interface is used to get the corresponding stored value based on hexadecimal contract address and stored key.

### Parameters

| Parameter        | Type  | Description                  |
| :--------------: | :---: | :--------------------------: |
| contract_address | str   | hexadecimal contract address |
| key              | str   | hexadecimal stored key       |

### Return Value

| Type  | Description                                                       |
| :---: | :---------------------------------------------------------------: |
| int   | the stored value according to the contract address and stored key |

## network.get_smart_contract_event_by_tx_hash

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
tx_hash = "65d3b2d3237743f21795e344563190ccbe50e9930520b8525142b075433fdd74"
event = sdk.rpc.get_smart_contract_event_by_tx_hash(tx_hash)
```

This interface is used to get the corresponding smart contract event based on the hexadecimal transaction hash value.

### Parameters

| Parameter | Type  | Description                        |
| :-------: | :---: | :--------------------------------: |
| tx_hash   | str   | hexadecimal transaction hash value |

### Return Value

| Type  | Description                                                |
| :---: | :--------------------------------------------------------: |
| dict  | the information of smart contract event in dictionary form |

## network.get_smart_contract_event_by_height

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
height = 0
event = sdk.rpc.get_smart_contract_event_by_height(height)
```

This interface is used to get the corresponding smart contract event based on the height of block.

### Parameters

| Parameter | Type  | Description            |
| :-------: | :---: | :--------------------: |
| height    | int   | a decimal height value |

### Return Value

| Type  | Description                                                |
| :---: | :--------------------------------------------------------: |
| dict  | the information of smart contract event in dictionary form |

## network.get_raw_transaction

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
tx_hash = "65d3b2d3237743f21795e344563190ccbe50e9930520b8525142b075433fdd74"
tx = sdk.rpc.get_raw_transaction(tx_hash)
```

This interface is used to get the corresponding transaction information based on the specified hash value.

### Parameters

| Parameter | Type  | Description                        |
| :-------: | :---: | :--------------------------------: |
| tx_hash   | str   | hexadecimal transaction hash value |

### Return Value

| Type  | Description                                       |
| :---: | :-----------------------------------------------: |
| dict  | the information of transaction in dictionary form |

## network.get_smart_contract

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
contract_address = "0239dcf9b4a46f15c5f23f20d52fac916a0bac0d"
contract = sdk.rpc.get_smart_contract(contract_address)
```

This interface is used to get the information of smart contract based on the specified hexadecimal hash value.

### Parameters

| Parameter        | Type  | Description            |
| :--------------: | :---: | :--------------------: |
| contract_address | str   | hexadecimal hash value |

### Return Value

| Type  | Description                                          |
| :---: | :--------------------------------------------------: |
| dict  | the information of smart contract in dictionary form |

## network.get_merkle_proof

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
tx_hash = "65d3b2d3237743f21795e344563190ccbe50e9930520b8525142b075433fdd74"
proof = sdk.rpc.get_merkle_proof(tx_hash)
```

This interface is used to get the corresponding merkle proof based on the specified hexadecimal hash value.

### Parameters

| Parameter | Type  | Description                        |
| :-------: | :---: | :--------------------------------: |
| tx_hash   | str   | hexadecimal transaction hash value |


### Return Value

| Type  | Description                         |
| :---: | :---------------------------------: |
| dict  | the merkle proof in dictionary form |

## network.send_raw_transaction

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
pri_key_1 = '75de8489fcb2dcaf2ef3cd607feffde18789de7da129b5e97c81e001793cb7cf'
acct = Account(pri_key_1)
length = 64
pri_key_2 = get_random_str(length)
acct2 = Account(pri_key_2)
b58_address_1 = acct.get_address_base58()
b58_address_2 = acct2.get_address_base58()
tx = Asset.new_transfer_transaction("ont", b58_address_1, b58_address_2, 2, b58_address_1, 20000, 500)
tx = sdk.sign_transaction(tx, acct)
tx_hash = sdk.rpc.send_raw_transaction(tx)
```

This interface is used to send the transaction into the network.

### Parameters

| Parameter | Type        | Description                                 |
| :-------: | :---------: | :-----------------------------------------: |
| tx        | Transaction | a Transaction object in ontology Python SDK |

### Return Value

| Parameter | Type  | Description                        |
| :-------: | :---: | :--------------------------------: |
| tx_hash   | str   | hexadecimal transaction hash value |

## network.send_raw_transaction_pre_exec

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
pri_key_1 = '75de8489fcb2dcaf2ef3cd607feffde18789de7da129b5e97c81e001793cb7cf'
acct = Account(pri_key_1)
pri_key2 = get_random_str(64)
acct2 = Account(pri_key2)
b58_address_1 = acct.get_address_base58()
b58_address_2 = acct2.get_address_base58()
tx = Asset.new_transfer_transaction("ont", b58_address_1, b58_address_2, 2, b58_address_1, 20000, 500)
tx = sdk.sign_transaction(tx, acct)
result = sdk.rpc.send_raw_transaction_pre_exec(tx)
```

This interface is used to send the transaction that is prepare to execute.

### Parameters

| Parameter | Type        | Description                                 |
| :-------: | :---------: | :-----------------------------------------: |
| tx        | Transaction | a Transaction object in ontology Python SDK |

### Return Value

| Type  | Description                                                    |
| :---: | :------------------------------------------------------------: |
| str   | the execution result of transaction that is prepare to execute |

# Wallet

## import_account

```python
wm = WalletManager()
path = os.path.join(os.getcwd(), 'test.json')
wm.open_wallet(path)
label = 'label'
encrypted_pri_key = 'Yl1e9ugbVADd8a2SbAQ56UfUvr3e9hD2eNXAM9xNjhnefB+YuNXDFvUrIRaYth+L'
password = '1'
b58_address = 'AazEvfQPcQ2GEFFPLF1ZLwQ7K5jDn81hve'
b64_salt = 'pwLIUKAf2bAbTseH/WYrfQ=='
wm.import_account(label, encrypted_pri_key, password, b58_address, b64_salt)
```

This interface is used to import account by providing account data.

### Parameters

| Parameter              | Type  | Description                                                               |
| :--------------------: | :---: | :-----------------------------------------------------------------------: |
| label                  | str   | wallet label                                                              |
| encrypted_pri_key: str | str   | an encrypted private key in base64 encoding from                          |
| pwd                    | str   | a password which is used to encrypt and decrypt the private key           |
| base58_address         | str   | a base58 encode  wallet address value                                     |
| base64_salt            | str   | a base64 encode salt value which is used in the encryption of private key |

### Return Value

| Type        | Description                                                                            |
| :---------: | :------------------------------------------------------------------------------------: |
| AccountData | if succeed, return an data structure which contain the information of a wallet account |
| None        | if failed, return a None object                                                        |

## create_account

```python
wm = WalletManager()
label = 'label'
password = 'password'
wm.create_account(label, password)
accounts = wm.get_wallet().get_accounts()
```

This interface is used to create account by seeting password and label.

### Parameters

| Parameter              | Type  | Description                                                               |
| :--------------------: | :---: | :-----------------------------------------------------------------------: |
| label                  | str   | wallet label                                                              |
| encrypted_pri_key: str | str   | an encrypted private key in base64 encoding from                          |
| pwd                    | str   | a password which is used to encrypt and decrypt the private key           |
| base58_address         | str   | a base58 encode  wallet address value                                     |
| base64_salt            | str   | a base64 encode salt value which is used in the encryption of private key |

### Return Value

| Type        | Description                                                                            |
| :---------: | :------------------------------------------------------------------------------------: |
| AccountData | if succeed, return an data structure which contain the information of a wallet account |
| None        | if failed, return a None object                                                        |

## create_account_from_private_key

```python
wm = WalletManager()
private_key = util.get_random_str(64)
label = 'hello_account'
password = 'password'
account = wm.create_account_from_private_key(label, password, private_key)
account_address = account.get_address()
```

This interface is used to create account by providing an encrypted private key and it's decrypt password.

# Message

# Smart Contract

## OEP4

### OEP4.get_name

```python
from ontology.ont_sdk import OntologySdk
sdk = OntologySdk()
remote_rpc_address = "http://polaris3.ont.io:20336"
sdk.set_rpc(remote_rpc_address)
contract_address = '6fe70af535887a820a13cfbaff6b0b505f855e5c'
oep4 = sdk.neo_vm().oep4()
oep4.set_contract_address(contract_address)
oep4.get_name()
```

This interface is used to call the `Name` method in ope4 that return the name of an oep4 token.

#### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

#### Return Value

| Type  | Description                        |
| :---: | :--------------------------------: |
| str   | the string name of the oep4 token. |

### OEP4.get_symbol

```python
from ontology.ont_sdk import OntologySdk
sdk = OntologySdk()
remote_rpc_address = "http://polaris3.ont.io:20336"
sdk.set_rpc(remote_rpc_address)
contract_address = '6fe70af535887a820a13cfbaff6b0b505f855e5c'
oep4 = sdk.neo_vm().oep4()
oep4.set_contract_address(contract_address)
oep4.get_symbol()
```

This interface is used to call the `Symbol` method in ope4 that return the symbol of an oep4 token.

#### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

#### Return Value

| Type  | Description                             |
| :---: | :-------------------------------------: |
| str   | a short string symbol of the oep4 token |

### OEP4.get_decimal

```python
from ontology.ont_sdk import OntologySdk
sdk = OntologySdk()
remote_rpc_address = "http://polaris3.ont.io:20336"
sdk.set_rpc(remote_rpc_address)
contract_address = '6fe70af535887a820a13cfbaff6b0b505f855e5c'
oep4 = sdk.neo_vm().oep4()
oep4.set_contract_address(contract_address)
oep4.get_decimal()
```

This interface is used to call the `Decimal` method in ope4 that return the number of decimals used by the oep4 token.

#### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

#### Return Value

| Type  | Description                                    |
| :---: | :--------------------------------------------: |
| int   | the number of decimals used by the oep4 token. |

### OEP4.init()

```python
from ontology.ont_sdk import OntologySdk
sdk = OntologySdk()
remote_rpc_address = "http://polaris3.ont.io:20336"
sdk.set_rpc(remote_rpc_address)
contract_address = '6fe70af535887a820a13cfbaff6b0b505f855e5c'
oep4 = sdk.neo_vm().oep4()
oep4.set_contract_address(contract_address)
private_key = '523c5fcf74823831756f0bcb3634234f10b3beb1c05595058534577752ad2d9f'
acct = Account(private_key, SignatureScheme.SHA256withECDSA)
gas_limit = 20000000
gas_price = 500
tx_hash = oep4.init(acct, acct, gas_limit, gas_price)
```

#### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

#### Return Value

| Type  | Description |
| :---: | :---------: |
|       |             |

### OEP4.get_total_supply()

```python
from ontology.ont_sdk import OntologySdk
sdk = OntologySdk()
remote_rpc_address = "http://polaris3.ont.io:20336"
sdk.set_rpc(remote_rpc_address)
contract_address = '6fe70af535887a820a13cfbaff6b0b505f855e5c'
oep4 = sdk.neo_vm().oep4()
oep4.set_contract_address(contract_address)
oep4.get_total_supply()
```

This interface is used to call the TotalSupply method in ope4 that return the total supply of the oep4 token.

#### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

#### Return Value

| Type  | Description                        |
| :---: | :--------------------------------: |
| int   | the total supply of the oep4 token |

### OEP4.balance_of()

```python
from ontology.ont_sdk import OntologySdk
sdk = OntologySdk()
remote_rpc_address = "http://polaris3.ont.io:20336"
sdk.set_rpc(remote_rpc_address)
contract_address = '6fe70af535887a820a13cfbaff6b0b505f855e5c'
oep4 = sdk.neo_vm().oep4()
oep4.set_contract_address(contract_address)
private_key = "523c5fcf74823831756f0bcb3634234f10b3beb1c05595058534577752ad2d9f"
acct = Account(private_key, SignatureScheme.SHA256withECDSA)
b58_address = acct.get_address_base58()
balance = oep4.balance_of(b58_address)
```

This interface is used to call the BalanceOf method in ope4 that query the ope4 token balance of the given base58 encode address.

#### Parameters

| Parameter   | Type  | Description               |
| :---------: | :---: | :-----------------------: |
| b58_address | str   | the base58 encode address |

#### Return Value

| Type  | Description                                         |
| :---: | :-------------------------------------------------: |
| int   | the oep4 token balance of the base58 encode address |

### OEP4.transfer()

```python
from ontology.ont_sdk import OntologySdk
sdk = OntologySdk()
remote_rpc_address = "http://polaris3.ont.io:20336"
sdk.set_rpc(remote_rpc_address)
contract_address = '6fe70af535887a820a13cfbaff6b0b505f855e5c'
oep4 = sdk.neo_vm().oep4()
oep4.set_contract_address(contract_address)

```

This interface is used to call the Transfer method in ope4 that transfer an amount of tokens from one account to another account.

#### Parameters

| Parameter      | Type    | Description                                                                                |
| :------------: | :-----: | :----------------------------------------------------------------------------------------: |
| from_acct      | Account | an Account class that send the oep4 token                                                  |
| b58_to_address | str     | a base58 encode address that receive the oep4 token                                        |
| value          | int     | an int value that indicate the amount oep4 token that will be transfer in this transaction |
| payer_acct     | Account | an Account class that used to pay for the transaction                                      |
| gas_limit      | int     | an int value that indicate the gas limit                                                   |
| gas_price      | int     | an int value that indicate the gas price                                                   |

#### Return Value

| Type  | Description                            |
| :---: | :------------------------------------: |
| str   | the hexadecimal transaction hash value |

### OEP4.transfer_multi()

```python
from ontology.ont_sdk import OntologySdk
sdk = OntologySdk()
remote_rpc_address = "http://polaris3.ont.io:20336"
sdk.set_rpc(remote_rpc_address)
contract_address = '6fe70af535887a820a13cfbaff6b0b505f855e5c'
oep4 = sdk.neo_vm().oep4()
oep4.set_contract_address(contract_address)
private_key1 = "523c5fcf74823831756f0bcb3634234f10b3beb1c05595058534577752ad2d9f"
private_key2 = "75de8489fcb2dcaf2ef3cd607feffde18789de7da129b5e97c81e001793cb7cf"
private_key3 = "1383ed1fe570b6673351f1a30a66b21204918ef8f673e864769fa2a653401114"
acct1 = Account(private_key1, SignatureScheme.SHA256withECDSA)
acct2 = Account(private_key2, SignatureScheme.SHA256withECDSA)
acct3 = Account(private_key3, SignatureScheme.SHA256withECDSA)
args = list()

b58_from_address1 = acct1.get_address_base58()
b58_from_address2 = acct2.get_address_base58()

b58_to_address1 = acct2.get_address_base58()
b58_to_address2 = acct3.get_address_base58()

value_list = [1, 2]

transfer1 = [b58_from_address1, b58_to_address1, value_list[0]]
transfer2 = [b58_from_address2, b58_to_address2, value_list[1]]
signers = [acct1, acct2, acct3]
args.append(transfer1)
args.append(transfer2)

gas_limit = 20000000
gas_price = 500

tx_hash = oep4.transfer_multi(args, signers[0], signers, gas_limit, gas_price)
```

#### Parameters

| Parameter  | Type    | Description                                                                                                                                                                  |
| :--------: | :-----: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| args       | list    | a parameter list with each item contains three sub-items:base58 encode transaction sender address,base58 encode transaction receiver address, amount of token in transaction |
| payer_acct | Account | an Account class that used to pay for the transaction                                                                                                                        |
| signers    | list    | a signer list used to sign this transaction which should contained all sender in args                                                                                        |
| gas_limit  | int     | an int value that indicate the gas limit                                                                                                                                     |
| gas_price  | int     | an int value that indicate the gas price                                                                                                                                     |

#### Return Value

| Type  | Description                            |
| :---: | :------------------------------------: |
| str   | the hexadecimal transaction hash value |

### OEP4.approve()

```python
from ontology.ont_sdk import OntologySdk
sdk = OntologySdk()
remote_rpc_address = "http://polaris3.ont.io:20336"
sdk.set_rpc(remote_rpc_address)
contract_address = '6fe70af535887a820a13cfbaff6b0b505f855e5c'
oep4 = sdk.neo_vm().oep4()
oep4.set_contract_address(contract_address)
private_key1 = "523c5fcf74823831756f0bcb3634234f10b3beb1c05595058534577752ad2d9f"
private_key2 = "75de8489fcb2dcaf2ef3cd607feffde18789de7da129b5e97c81e001793cb7cf"
owner_acct = Account(private_key1, SignatureScheme.SHA256withECDSA)
spender = Account(private_key2, SignatureScheme.SHA256withECDSA)
payer_acct = owner_acct
b58_spender_address = spender.get_address_base58()
amount = 100
gas_limit = 20000000
gas_price = 500
tx_hash = oep4.approve(owner_acct, b58_spender_address, amount, payer_acct, gas_limit, gas_price)
```

This interface is used to call the Approve method in ope4 that allows spender to withdraw a certain amount of oep4 token from owner account multiple times.

**Attention**: If this function is called again, it will overwrite the current allowance with new value.

#### Parameters

| Parameter           | Type    | Description                                                                                |
| :-----------------: | :-----: | :----------------------------------------------------------------------------------------: |
| owner_acct          | Account | an Account class that indicate the owner                                                   |
| b58_spender_address | str     | a base58 encode address that be allowed to spend the oep4 token in owner's account         |
| amount              | int     | an int value that indicate the amount oep4 token that will be transfer in this transaction |
| payer_acct          | Account | an Account class that used to pay for the transaction                                      |
| gas_limit           | int     | an int value that indicate the gas limit                                                   |
| gas_price           | int     | an int value that indicate the gas price                                                   |

#### Return Value

| Type  | Description                            |
| :---: | :------------------------------------: |
| str   | the hexadecimal transaction hash value |

### OEP4.allowance()

```python
from ontology.ont_sdk import OntologySdk
sdk = OntologySdk()
remote_rpc_address = "http://polaris3.ont.io:20336"
sdk.set_rpc(remote_rpc_address)
contract_address = '6fe70af535887a820a13cfbaff6b0b505f855e5c'
oep4 = sdk.neo_vm().oep4()
oep4.set_contract_address(contract_address)

```

#### Parameters

| Parameter           | Type  | Description                                              |
| :-----------------: | :---: | :------------------------------------------------------: |
| b58_owner_address   | str   | a base58 encode address that represent owner's account   |
| b58_spender_address | str   | a base58 encode address that represent spender's account |

#### Return Value

| Type  | Description                                                                          |
| :---: | :----------------------------------------------------------------------------------: |
| int   | the amount of oep4 token that owner allow spender to transfer from the owner account |

### OEP4.transfer_from()

```python
from ontology.ont_sdk import OntologySdk
sdk = OntologySdk()
remote_rpc_address = "http://polaris3.ont.io:20336"
sdk.set_rpc(remote_rpc_address)
contract_address = '6fe70af535887a820a13cfbaff6b0b505f855e5c'
oep4 = sdk.neo_vm().oep4()
oep4.set_contract_address(contract_address)
private_key1 = "523c5fcf74823831756f0bcb3634234f10b3beb1c05595058534577752ad2d9f"
private_key2 = "75de8489fcb2dcaf2ef3cd607feffde18789de7da129b5e97c81e001793cb7cf"
private_key3 = "1383ed1fe570b6673351f1a30a66b21204918ef8f673e864769fa2a653401114"
spender_acct = Account(private_key2, SignatureScheme.SHA256withECDSA)
from_acct = Account(private_key1, SignatureScheme.SHA256withECDSA)
to_acct = Account(private_key3, SignatureScheme.SHA256withECDSA)
b58_to_address = to_acct.get_address_base58()
gas_limit = 20000000
gas_price = 500
value = 1
tx_hash = oep4.transfer_from(spender_acct, from_acct, b58_to_address, value, from_acct, gas_limit, gas_price)
```

#### Parameters

| Parameter      | Type    | Description                                                               |
| :------------: | :-----: | :-----------------------------------------------------------------------: |
| spender_acct   | Account | an Account class that spend the oep4 token.                               |
| from_acct      | Account | an Account class that actually pay oep4 token for the spender's spending. |
| b58_to_address | str     | a base58 encode address that receive the oep4 token.                      |
| value          | int     | the amount of ope4 token in this transaction.                             |
| payer_acct     | Account | an Account class that used to pay for the transaction.                    |
| gas_limit      | int     | an int value that indicate the gas limit.                                 |
| gas_price      | int     | an int value that indicate the gas price.                                 |

#### Return Value

| Type  | Description                            |
| :---: | :------------------------------------: |
| str   | the hexadecimal transaction hash value |