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

## sdk.rpc.get_current_block_hash

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
current_block_hash = sdk.rpc.get_current_block_hash()
```

This interface is used to get block by block hash.

### Parameters

| Parameter | Type   | Description           |
| --------- | ------ | --------------------- |
|           |        |                       |

### Return Value

dict

## sdk.rpc.get_block_hash_by_height

```python

from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
hash = '44425ae42a394ec0c5f3e41d757ffafa790b53f7301147a291ab9b60a956394c'
block_hash = sdk.rpc.get_block_hash_by_height(0)
```

## sdk.rpc.get_version()

```python
from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
version = sdk.rpc.get_version()
```

## sdk.rpc.get_block_by_hash

```python
from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
hash = "44425ae42a394ec0c5f3e41d757ffafa790b53f7301147a291ab9b60a956394c"
block = sdk.rpc.get_block_by_hash(hash)
```

## sdk.rpc.get_block_by_height

```python
from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
height = 0
block = sdk.rpc.get_block_by_hash(height)
```

## sdk.rpc.get_block_count

```python
from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
count = sdk.rpc.get_block_count()
```

## sdk.rpc.get_current_block_hash

```python
from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
current_block_hash = sdk.rpc.get_current_block_hash()
```

## sdk.rpc.get_block_hash_by_height ()

```python
from ontology.ont_sdk import OntologySdk

rpc_address = 'http://polaris3.ont.io:20336'
sdk = OntologySdk()
sdk.rpc.set_address(rpc_address)
height = 0
block_hash = sdk.rpc.get_block_hash_by_height(height)
```

## sdk.rpc.get_balance ()

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

## sdk.rpc.get_allowance ()

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

## sdk.rpc.get_storage ()

## sdk.rpc.get_smart_contract_event_by_txhash ()

## sdk.rpc.get_smart_contract_event_by_block ()

## sdk.rpc.get_raw_transaction ()

## sdk.rpc.get_smart_contract ()

## sdk.rpc.get_merkle_proof ()

## send_raw_transaction ()

## send_raw_transaction_preexec ()

