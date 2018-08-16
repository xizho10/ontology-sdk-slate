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

# RPC interface function

## sdk.rpc.get_version

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

## sdk.rpc.get_block_by_hash

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

| Parameter  | Type  | Description                    |
| :--------: | :---: | :----------------------------: |
| block_hash | str   | a hexadecimal block hash value |

### Return Value

| Type  | Description                                       |
| :---: | :-----------------------------------------------: |
| dict  | the block information of the specified block hash |

## sdk.rpc.get_block_by_height

```python
from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
height = 0
block = sdk.rpc.get_block_by_hash(height)
```

This interface is used to get the block information by block height in current network.

### Parameters

| Parameter | Type  | Description            |
| :-------: | :---: | :--------------------: |
| height    | int   | a decimal height value |

### Return Value

| Type  | Description                                         |
| :---: | :-------------------------------------------------: |
| dict  | the block information of the specified block height |

## sdk.rpc.get_block_count

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

| Type  | Description                      |
| :---: | :------------------------------: |
| int   | a decimal total number of blocks |

## sdk.rpc.get_current_block_hash

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

| Type  | Description                                                      |
| :---: | :--------------------------------------------------------------: |
| dict  | a hexadecimal hash value of the highest block in current network |

## sdk.rpc.get_block_hash_by_height

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

| Type  | Description                                            |
| :---: | :----------------------------------------------------: |
| str   | a hexadecimal hash value of the specified block height |

## sdk.rpc.get_balance()

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

| Type  | Description                                       |
| :---: | :-----------------------------------------------: |
| dict  | an account balance value saved in dictionary form |

## sdk.rpc.get_allowance

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

| Type  | Description                                                            |
| :---: | :--------------------------------------------------------------------: |
| str   | the decimal allowance from transfer-from accout to transfer-to account |

## sdk.rpc.get_storage

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
contract_address = "0100000000000000000000000000000000000000"
key = "746f74616c537570706c79"
value = sdk.rpc.get_storage(contract_address, key)
```

This interface is used to get the corresponding stored value according based on hexadecimal contract address and stored key.

### Parameters

| Parameter        | Type  | Description                  |
| :--------------: | :---: | :--------------------------: |
| contract_address | str   | hexadecimal contract address |
| key              | str   | hexadecimal stored key       |

### Return Value

| Type  | Description                                                       |
| :---: | :---------------------------------------------------------------: |
| int   | the stored value according to the contract address and stored key |

## sdk.rpc.get_smart_contract_event_by_tx_hash

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
tx_hash = "65d3b2d3237743f21795e344563190ccbe50e9930520b8525142b075433fdd74"
event = sdk.rpc.get_smart_contract_event_by_tx_hash(tx_hash)
```

This interface is used to get the corresponding smart contract event based on the hexadecimal transaction hash vlaue.

### Parameters

| Parameter | Type  | Description                        |
| :-------: | :---: | :--------------------------------: |
| tx_hash   | str   | hexadecimal transaction hash vlaue |

### Return Value

| Type  | Description              |
| :---: | :----------------------: |
| dict  | the smart contract event |

## sdk.rpc.get_smart_contract_event_by_height

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
height = 0
event = sdk.rpc.get_smart_contract_event_by_height(height)
```

This interface is used to get the corresponding smart contract event based on the height of block.

## sdk.rpc.get_raw_transaction

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
| tx_hash   | str   | hexadecimal transaction hash vlaue |

### Return Value

| Type  | Description                                    |
| :---: | :--------------------------------------------: |
| dict  | the transaction information in dictionary form |

## sdk.rpc.get_smart_contract

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
contract_address = "0239dcf9b4a46f15c5f23f20d52fac916a0bac0d"
contract = sdk.rpc.get_smart_contract(contract_address)
```

This interface is used to get the corresponding merkle proof based on the specified hexadecimal hash value.

### Parameters

| Parameter        | Type  | Description            |
| :--------------: | :---: | :--------------------: |
| contract_address | str   | hexadecimal hash value |

### Return Value

## sdk.rpc.get_merkle_proof

### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

This interface is used to get the corresponding transaction information based on the hexadecimal transaction hash

### Return Value


## sdk.rpc.get_smart_contract_event_by_txhash ()

### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

### Return Value


## sdk.rpc.get_smart_contract_event_by_block ()

### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

### Return Value


## sdk.rpc.get_raw_transaction ()

### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

### Return Value


## sdk.rpc.get_smart_contract ()

### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

### Return Value


## sdk.rpc.get_merkle_proof ()

### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

### Return Value


## send_raw_transaction ()

### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

### Return Value


## send_raw_transaction_preexec ()

### Parameters

| Parameter | Type  | Description |
| :-------: | :---: | :---------: |
|           |       |             |

### Return Value

