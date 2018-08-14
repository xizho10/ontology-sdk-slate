---
title: Ontology Smart Contract API Reference

language_tabs: # must be one of 
  - c#
  - python

toc_footers:
  - <a href='https://github.com/ontio/ontology-smartcontract/'>Check for more examples</a>
  - <a href='https://ont.io'>Powered by Ontology</a>

includes:
 

search: false
---

# Introduction

The API of smart contract defines the interfaces between the smart contract program and the ledger layer. These interfaces provide functions that can access data in the blockchain ledger, persistent storage, smart contracts, and native contracts. These interfaces can be roughly divided into four categories.

1. Blockchain ledger: A contract program can use the API of smart contract to access all data in the blockchain ledger including transaction information, block information, smart contract information, and so on.

2. Persistent storage: A smart contract deployed on the blockchain can operate its own storage area such as adding, updating, querying, and deleting its storage area. 

3. Smart contract: A contract program can use the API of smart contract to create, update, and delete a contract.

4. Native contract: The Ontology provides a series of native contract services including OntID contract, Auth contract, Ont contract, Ong contract, and so on. They can access basic services of Ontology through the native contract interface.

# Blockchain

This class provides a set of methods for accessing blockchain data.

## Blockchain.GetHeight

```csharp

using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
{
     public static void Main()
     {
         uint height = Blockchain.GetHeight();
     }
}
}
```

This interface is used to get current block height.

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

uint

## Blockchain.GetHeader

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            Header header = Blockchain.GetHeader(9999);
        }
    }
}
```

This interface is used to get block header by height.

### Parameters

| Parameter | Type | Description     |
| --------- | ---- | --------------- |
| height    | uint | header of block |

### Return Value

Header

## Blockchain.GetBlock

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            byte[] block = new byte[] {206, 240, 165, 25, 76, 228, 58, 100, 117, 184, 213, 171, 61, 96, 34, 234, 129, 116, 60, 71, 11, 231, 143, 195, 123, 5, 190, 250, 182, 14, 152};
            Block bl = Blockchain.GetBlock(block);
        }
    }
}
```

This interface is used to get block by block hash.

### Parameters

| Parameter | Type   | Description           |
| --------- | ------ | --------------------- |
| hash      | byte[] | The hash of the block |

### Return Value

Block

## Blockchain.GetTransaction

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
         public static void Main()
         {
             byte[] txid = new byte[] {206, 240, 165, 25, 76, 228, 58, 100, 117, 184, 213, 171, 61, 96, 34, 234, 129, 116, 60, 71, 11, 231, 143, 195, 123, 5, 190, 250, 182, 14, 152};
             Transaction transaction = Blockchain.GetTransaction(txid);
         }
    }
}
```

This interface is used to get transaction by transaction hash.

### Parameters

| Parameter | Type   | Description               |
| --------- | ------ | ------------------------- |
| txid      | byte[] | The id of the transaction |

### Return Value

Transaction

## Blockchain.GetContract

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
         public static void Main()
         {
             byte[] script_hash = new byte[] {206, 240, 165, 25, 76, 228, 58, 100, 117, 184, 213, 171, 61, 96, 34, 234, 129, 116, 60, 71, 11, 231, 143, 195, 123, 5, 190, 250, 182, 14, 152};
             Contract contract = Blockchain.GetContract(script_hash);
         }
    }
}
```

This method is to get contract by contract hash.

### Parameters

| Parameter   | Type   | Description                     |
| ----------- | ------ | ------------------------------- |
| script_hash | byte[] | The script hash of the contract |

### Return Value

Contract

## Blockchain.GetTransactionHeight

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
{
     public static void Main()
     {
         byte[] txid = new byte[] {206, 240, 165, 25, 76, 228, 58, 100, 117, 184, 213, 171, 61, 96, 34, 234, 129, 116, 60, 71, 11, 231, 143, 195, 123, 5, 190, 250, 182, 14, 152};
         uint height = Blockchain.GetTransactionHeight(txid);
     }
}
}
```

This interface is used to get height of transaction in block by transaction hash.

### Parameters

| Parameter | Type   | Description               |
| --------- | ------ | ------------------------- |
| txid      | byte[] | The id of the transaction |

### Return Value

uint

# Header

## Header.Hash

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
{
     public static void Main()
     {
         Header header = Blockchain.GetHeader(9999);
         byte[] hash = header.Hash;
     }
}

```

This interface is used to get hash of block

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |

### Return Value

byte[]



## Header.Version

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            Header header = Blockchain.GetHeader(9999);
            uint version = header.Version;
        }
    }
}
```

This interface is used to get block version number

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

uint



## Header.PrevHash

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            Header header = Blockchain.GetHeader(9999);
            byte[] prevHash = header.PrevHash;
        }
    }
}
```

This interface is used to get hash of previous block

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

byte[]



## Header.Index

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            Header header = Blockchain.GetHeader(9999);
            uint index = header.Index;
        }
     }
}
```

This interface is used to get height of block

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

uint



## Header.MerkleRoot

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            Header header = Blockchain.GetHeader(9999);
            byte[] mRoot = header.MerkleRoot;
        }
    }
}
```

This interface is used to get root of  Merkle Tree for all transactions in block

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

byte[]



## Header.Timestamp

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            Header header = Blockchain.GetHeader(9999);
            uint timestamp = header.Timestamp;
        }
    }
}
```

This interface is used to get block's timestamp

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

uint



## Header.ConsensusData

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            Header header = Blockchain.GetHeader(9999);
            ulong cdata = header.ConsensusData;
        }
    }
}
```

This interface is used to get block's consensusData

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

ulong



## Header.NextConsensus

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            Header header = Blockchain.GetHeader(9999);
            byte[] nextConsensus = header.NextConsensus;
        }
     }
}
```

This interface is used to get hash of next bookkeeping 

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

byte[]



# Block

## Block.GetTransactionCount()

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            byte[] block = new byte[] {206, 240, 165, 25, 76, 228, 58, 100, 117, 184, 213, 171, 61, 96, 34, 234, 129, 116, 60, 71, 11, 231, 143, 195, 123, 5, 190, 250, 182, 14, 152};
            Block bl = Blockchain.GetBlock(block);
            int count = bl.GetTransactionCount();
        }
     }
}
```

This interface is used to get the count of transactions in block

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

int


## Block.GetTransactions()

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            byte[] block = new byte[] {206, 240, 165, 25, 76, 228, 58, 100, 117, 184, 213, 171, 61, 96, 34, 234, 129, 116, 60, 71, 11, 231, 143, 195, 123, 5, 190, 250, 182, 14, 152};
            Block bl = Blockchain.GetBlock(block);
            Transaction[] transactions = bl.GetTransactions();
        }
    }
}
```

This interface is used to get all transactions in block

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

Transaction[]



## Block.GetTransaction(int index)

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            byte[] block = new byte[] {206, 240, 165, 25, 76, 228, 58, 100, 117, 184, 213, 171, 61, 96, 34, 234, 129, 116, 60, 71, 11, 231, 143, 195, 123, 5, 190, 250, 182, 14, 152};
            Block bl = Blockchain.GetBlock(block);
            Transaction transaction = bl.GetTransaction(1);
        }
    }
}
```

This interface is used to get  transaction according index in block

### Parameters

| Parameter | Type | Description                |
| --------- | ---- | -------------------------- |
| index     | int  | transaction index of block |

### Return Value

Transaction



# Transaction 

## Transaction.Hash

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            byte[] block = new byte[] {206, 240, 165, 25, 76, 228, 58, 100, 117, 184, 213, 171, 61, 96, 34, 234, 129, 116, 60, 71, 11, 231, 143, 195, 123, 5, 190, 250, 182, 14, 152};
            Block bl = Blockchain.GetBlock(block);
            Transaction transaction = bl.GetTransaction(1);
            byte[] hash = transaction.Hash;
        }
    }
}

```

This interface is used to get hash of transaction

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

byte[]



## Transaction.Type

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            byte[] block = new byte[] {206, 240, 165, 25, 76, 228, 58, 100, 117, 184, 213, 171, 61, 96, 34, 234, 129, 116, 60, 71, 11, 231, 143, 195, 123, 5, 190, 250, 182, 14, 152};
            Block bl = Blockchain.GetBlock(block);
            Transaction transaction = bl.GetTransaction(1);
            byte ttype = transaction.Type;
        }
    }
}

```

This interface is used to get type of the current transaction

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

byte



## Transaction.GetAttributes()

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            byte[] block = new byte[] {206, 240, 165, 25, 76, 228, 58, 100, 117, 184, 213, 171, 61, 96, 34, 234, 129, 116, 60, 71, 11, 231, 143, 195, 123, 5, 190, 250, 182, 14, 152};
            Block bl = Blockchain.GetBlock(block);
            Transaction transaction = bl.GetTransaction(1);
            TransactionAttribute[] attributes = transaction.GetAttributes();
        }
    }
}

```

This interface is used to get attributes of transaction

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

TransactionAttribute[]



# Contract

## Contract.Script

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            byte[] script_hash = new byte[] {206, 240, 165, 25, 76, 228, 58, 100, 117, 184, 213, 171, 61, 96, 34, 234, 129, 116, 60, 71, 11, 231, 143, 195, 123, 5, 190, 250, 182, 14, 152};
            Contract contract = Blockchain.GetContract(script_hash);
            byte[] scrip = contract.Script;
        }
    }
}
```

This interface is used to get script of contract according to contract script hash.

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

byte[]



## Contract.Create

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            byte[] script = new byte[] { 116, 107, 0, 97, 116, 0, 147, 108, 118, 107, 148, 121, 116, 81, 147, 108, 118, 107, 148, 121, 147, 116, 0, 148, 140, 108, 118, 107, 148, 114, 117, 98, 3, 0, 116, 0, 148, 140, 108, 118, 107, 148, 121, 97, 116, 140, 108, 118, 107, 148, 109, 116, 108, 118, 140, 107, 148, 109, 116, 108, 118, 140, 107, 148, 109, 108, 117, 102 }; 

            byte[] parameter_list = { 2, 2 };
            byte return_type = 2;
            bool need_storage = false;
            string name = "contractName";
            string version = "1";
            string author = "test";
            string email = "test@ont.io";
            string description = "this is a test contract";
        
            Contract contract = Contract.Create(script, true,name,version,author,email,description);
        }
    }
}
```

This interface is used to create a smart contract

### Parameters

| Parameter    | Type   | Description                  |
| ------------ | ------ | ---------------------------- |
| script       | byte[] | contract script bytes        |
| need_storage | bool   | contract need storage or not |
| name         | string | contract name                |
| version      | string | contract version             |
| author       | string | contract author              |
| email        | string | contract email               |
| desc         | string | contract description         |

### Return Value

Contract



## Contract.Migrate

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main(byte[] signature)
        {
            byte[] script = new byte[] { 116, 107, 0, 97, 116, 0, 147, 108, 118, 107, 148, 121, 116, 81, 147, 108, 118, 107, 148, 121, 147, 116, 0, 148, 140, 108, 118, 107, 148, 114, 117, 98, 3, 0, 116, 0, 148, 140, 108, 118, 107, 148, 121, 97, 116, 140, 108, 118, 107, 148, 109, 116, 108, 118, 140, 107, 148, 109, 116, 108, 118, 140, 107, 148, 109, 108, 117, 102 }; 
        
            byte[] parameter_list = { 2, 2 };
            byte return_type = 2;
            bool need_storage = true;
            string name = "contractName";
            string version = "1";
            string author = "test";
            string email = "test@ont.io";
            string description = "this is a test contract";
        
            Contract contract = Contract.Migrate(script, true,name,version,author,email,description);
         }
    }
}

```

This interface is used to migrate / update a smart contract,it should be implemented in contract which need to migrate.old contract storage will automatic migrate to new contract.
 
### Parameters

| Parameter    | Type   | Description                  |
| ------------ | ------ | ---------------------------- |
| script       | byte[] | contract script bytes        |
| need_storage | bool   | contract need storage or not |
| name         | string | contract name                |
| version      | string | contract version             |
| author       | string | contract author              |
| email        | string | contract email               |
| desc         | string | contract description         |

### Return Value

Contract



## Contract.Destroy()

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            Contract.Destroy();
        }
    }
}
```

This interface is used to destroy a contract.script and storage of contract will be removed.

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

void



## Contract.StorageContext

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
{
     public static void Main()
     {
          byte[] script_hash = new byte[] {206, 240, 165, 25, 76, 228, 58, 100, 117, 184, 213, 171, 61, 96, 34, 234, 129, 116, 60, 71, 11, 231, 143, 195, 123, 5, 190, 250, 182, 14, 152};
         Contract contract = Blockchain.GetContract(script_hash);
         StorageContext sc = contract.StorageContext;
     }
}

```

This interface is used to get the contract's storage context

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

StorageContext



# Storage

## Storage.CurrentContext

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
{
     public static void Main()
     {
         StorageContext sc = Storage.CurrentContext;
     }
}

```

This interface is used to get current storage context

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

StorageContext



## Storage.Get(StorageContext,byte[])

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
{
     public static void Main()
     {
         StorageContext sc = Storage.CurrentContext;
         byte[] key = new byte[] {97, 98,99};
         byte[] val = Storage.Get(sc,key);
     }
}

```

This interface is used to get value by key in current smart contract.

### Parameters

| Parameter | Type           | Description     |
| --------- | -------------- | --------------- |
| sc        | StorageContext | storage context |
| key       | byte[]         | storage key     |

### Return Value

byte[]



## Storage.Get(StorageContext,string)

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
{
     public static void Main()
     {
         StorageContext sc = Storage.CurrentContext;
         string key = "key";
         byte[] val = Storage.Get(sc,key);
     }
}

```

This interface is used to get value by key in current smart contract.

### Parameters

| Parameter | Type           | Description     |
| --------- | -------------- | --------------- |
| sc        | StorageContext | storage context |
| key       | string         | storage key     |

### Return Value

byte[]



## Storage.Put(StorageContext,string/byte[],string/byte[])

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            StorageContext sc = Storage.CurrentContext;
            string key = "key";
            string val = "value";
            Storage.Put(sc,key,val);
        }
    }
}

```

This interface is used to insert operation, inserting data as key-value format into a persistent storage area

### Parameters

| Parameter | Type           | Description     |
| --------- | -------------- | --------------- |
| sc        | StorageContext | storage context |
| key       | string/byte[]  | storage key     |
| val       | string/byte[]  | storage value   |

### Return Value

void



## Storage.Delete(StorageContext,string/byte[])

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            StorageContext sc = Storage.CurrentContext;
            string key = "key";
            Storage.Delete(sc,key);
        }
    }
}

```

This interface is used to delete operation, delete the corresponding value by key in the persistent storage area

### Parameters

| Parameter | Type           | Description     |
| --------- | -------------- | --------------- |
| sc        | StorageContext | storage context |
| key       | string/byte[]  | storage key     |

### Return Value

void



# Runtime

## Runtime.Time

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            uint rtime = Runtime.Time;
        }
    }
}
```

This interface is used to get current block time

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

uint



## Runtime.CheckWitness(byte[])

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            byte[] pubKey = { 2, 123, 48, 51, 62, 13, 14, 101, 82, 174, 109, 29, 169, 249, 64, 159, 85, 30, 53, 238, 151, 25, 48, 94, 148, 93, 196, 220, 186, 153, 132, 86, 202 };
            bool result = Runtime.CheckWitness(pubKey);
        }
    }
}

```

This interface is used to verify operational permissions of account or contract

### Parameters

| Parameter | Type   | Description                   |
| --------- | ------ | ----------------------------- |
| pubkey    | byte[] | address of people or contract |

### Return Value

bool



## Runtime.Notify(object[])

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            Runtime.Notify("Hello", "World", Blockchain.GetHeight());
        }
    }
}

```

In smart contract, sending notifications (including socket notifications or rpc queries) to clients that are executing this smart contract.

### Parameters

| Parameter | Type     | Description     |
| --------- | -------- | --------------- |
| message   | object[] | notify messages |

### Return Value

void



## Runtime.Log(string)

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            Runtime.Log("Hello world");
        }
     }
}

```

 In smart contract, sending logs ( including socket notifications) to clients that are executing this smart contract.

### Parameters

| Parameter | Type   | Description  |
| --------- | ------ | ------------ |
| message   | string | log messages |

### Return Value

void



# ExecutionEngine

## ExecutionEngine.ScriptContainer

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;
using Ont.SmartContract.Framework.Services.System;

namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            IScriptContainer isc = ExecutionEngine.ScriptContainer;
        }
     }
}

```

This method is to get script container of a smart contract

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

IScriptContainer



## ExecutionEngine.ExecutingScriptHash

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;
using Ont.SmartContract.Framework.Services.System;

namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            byte[] scriptHash = ExecutionEngine.ExecutingScriptHash;
        }
    }
}

```

This interface is used to get current contract hash

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

byte[]



## ExecutionEngine.CallingScriptHash

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;
using Ont.SmartContract.Framework.Services.System;

namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            byte[] callingScriptHash = ExecutionEngine.CallingScriptHash;
        }
    }
}

```

This interface is used to get script hash of the invoker of a smart contract

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

byte[]



## ExecutionEngine.EntryScriptHash

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;
using Ont.SmartContract.Framework.Services.System;

namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static void Main()
        {
            byte[] entryScriptHash = ExecutionEngine.EntryScriptHash;
        }
    }
}

```

This interface is used to get  script hash of entry point (start of the contract invocation chain) of a smart contract

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

byte[]



# Native

## Native.Invoke(byte version, byte[] address, byte[] method, object args)

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;


namespace Contract1
{
    public class Contract1: SmartContract
    {
        public static readonly byte[] ontAddr = "AFmseVrdL9f9oyCzZefL9tG6UbvhUMqNMV".ToScriptHash();
        struct Transfer
        {
            public byte[] From;
            public byte[] To;
            public ulong Value;
        }
        public static bool Main()
        {

            byte[] from = { 2, 123, 48, 51, 62, 13, 14, 101, 82, 174, 109, 29, 169, 249, 64, 159, 85, 30, 53, 238, 151, 25, 48, 94, 148, 93, 196, 220, 186, 153, 132, 86, 202 };
            byte[] to = { 2, 123, 48, 51, 62, 13, 14, 101, 82, 174, 109, 29, 169, 249, 64, 159, 85, 30, 53, 238, 151, 25, 48, 94, 148, 93, 196, 220, 186, 153, 132, 86, 202 };
            ulong value = 100;
            Transfer param = new Transfer { From = from, To = to, Value = value };
            object[] p = new object[1];
            p[0] = param;
            byte[] ret = Native.Invoke(0, ontAddr, "transfer", p);
            if (ret[0] != 1)
            {
                return false;
            };
            return true;
        }
    }
}

```

Invokes a native contract. 1. version - version number， 2. address - contract address 3. method - contract method 4. contract parameters

### Parameters

| Parameter | Type | Description |
| --------- | ---- | ----------- |
|           |      |             |

### Return Value

byte[]



# Convert byte[] and String

```csharp
//convert string to byte[]
string a = "aaa";
byte[] b = (byte[])(object)a;

//or 
string a = "aaa";
byte[] b = a.AsByteArray();

//convert byte[] to string
byte[] a = {1, 2, 3};
string b = a.AsString();

```



# Using Map and Struct

You can use map and struct to store data as following

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;
using Ont.SmartContract.Framework.Services.System;
using System;
using System.ComponentModel;
using System.Numerics;
using System.Text;
using Helper = Ont.SmartContract.Framework.Helper;

namespace DID
{
    public class DID : SmartContract
    {
        public static Object Main(string operation, params object[] args)
        {
            if (operation == "TestMap")
            {
                return TestMap();
            }else if (operation == "DeserializeMap")
            {
                return DeserializeMap((byte[])args[0]);
            }
            else if (operation == "TestStruct")
            {
                return TestStruct();
            }
             else if(operation == "DeserializeStruct"){
                return DeserializeStruct((byte[])args[0]);
            }
            return null;
        }

        public static object TestMap()
        {
            StorageContext context = Storage.CurrentContext;
            Map<string, int> m = new Map<string, int>();
            int value = 100;
            //m["hello"] = "world";
            m["key"] = value;

            byte[] b = Helper.Serialize(m);
            Storage.Put(context, "tx", b);

            byte[] v = Storage.Get(context, "tx");

            Map<string, int> b2 = (Map<string, int>)Helper.Deserialize(v);

            //&& b2["hello"] == "world"
            if ( b2 != null  && (int)b2["key"] == value )
            {
                Storage.Put(context, "result", "true");
                return b;
            }

            Storage.Put(context, "result", "false");
            return false;
        }


        public static object DeserializeMap(byte[] param)
        {
            Map<string, int> b2 = (Map<string, int>)Helper.Deserialize(param);
            StorageContext context = Storage.CurrentContext;

            int value = 100;
            //&& b2["hello"] == "world"
            if (b2 != null  && (int)b2["key"] == value )
            {
                Storage.Put(context, "result", "true");
                return true;
            }

            Storage.Put(context, "result", "false");
            return (int)b2["key"];
        }
        
        public static object TestStruct()
        {
            StorageContext context = Storage.CurrentContext;
            ClaimTx m = new ClaimTx();
            m.name = "claimid";
            m.claimId = 100;

            byte[] b = Helper.Serialize(m);
            Storage.Put(context, "tx", b);

            byte[] v = Storage.Get(context, "tx");

            if(b != null){
              return b;
            }
 

            Storage.Put(context, "result", "false");
            return false;
        }
        public static object DeserializeStruct(byte[] param)
        {
            ClaimTx b2 = (ClaimTx)Helper.Deserialize(param);
            StorageContext context = Storage.CurrentContext;

            int value = 100;
            //&& b2["hello"] == "world"
            if (b2 != null  && (int)b2.claimId == value )
            {
                Storage.Put(context, "result", "true");
                return true;
            }

            Storage.Put(context, "result", "false");
            return (int)b2.claimId;
        }
        public class ClaimTx
        {
            public int claimId;
            public string name;
        }
    }
}
```



# Action and Notify

Currently  action is not supported ,so you need to replace action with following event codes:

```csharp
using Ont.SmartContract.Framework;
using Ont.SmartContract.Framework.Services.Ont;
using Ont.SmartContract.Framework.Services.System;
using System;
using System.ComponentModel;
using System.Numerics;

namespace NeoContract3
{
    public class Contract1 : SmartContract
    {
        public delegate void TransferDel(byte[] from, byte[] to, BigInteger value);

        [DisplayName("transfer")]
        public static event TransferDel Transferred;

        public static Object Main(string operation, params object[] args)
        {
            if (operation == "Hello")
            {
                return Hello();
            }
            return false;

        }

        public static string Hello()
        {
            Storage.Put(Storage.CurrentContext, "Hello", "World");
            Transferred("hello".AsByteArray(), "world".AsByteArray(), 123);
            return "123";
        }
    }
}
```

 

# Calling other Smart Contract

 You can call other smart contracts from your contract:

```csharp
[Appcall("XXXXXXXXXX")]//ScriptHash
public static extern int AnotherContract(string arg);

public static void Main()
{
    AnotherContract("Hello");    
}

```

