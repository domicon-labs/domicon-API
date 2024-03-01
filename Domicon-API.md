### eth_uploadFileDataByParams

give geth a new DA data.

#### Parameters

- 1,2.sender,submitter 20 Bytes - sender: who send the DA;submitter: who broadcast the DA.
- 3.index integer - sender send DA index number.
- 4.length integer - DA length.
- 5.gasPrice integer - integer of the gasPrice used for each paid gas, in Wei..
- 6.commitment 48 Bytes - created by DA, we can match the commitment and DA by zkg algorithms.
- 7.data N Bytes - DA data.
- 8.signData N Bytes - signature.
- 9.txHash 32 Bytes - txHash of L1 transaction.

#### Returns

Error - if already receive no error will return.


### eth_uploadFileData

give geth a new DA data.

#### Parameters

- data N Bytes - DA rlp encode data.

#### Returns 

Error - if already receive no error will return.
 

### eth_checkSelfState

node can check themself if DA data is complete.

#### Parameters
 
 - blockNr - integer of a block number, or the string "earliest", "latest" or "pending"
 
#### Returns 
 
 Boolean - check node self have complete data or not.
 Error - error message.


### eth_getFileDataByHash 

get DA data by Txhash.

#### Parameters

- hash 32 Bytes - the L1 transaction hash.

#### Returns

Object - A DA object, or null when no DA was found:

- Sender: 32 Bytes - DA sender.
- Submmiter: 32 Bytes - broadcast DA data.
- Length: integer - DA data length.
- Index: integer - DA sender of index.
- Commitment: 48 Bytes - created by DA, we can match the commitment and DA by zkg algorithms.
- Data: N Bytes - DA data.
- Sign: N Bytes - signature.
- TxHash: 32 Bytes - txHash of L1 transaction.

### eth_getFileDataByCommitment 

get DA data by commitment.

#### Parameters

- comimt 48 Bytes - created by DA, we can match the commitment and DA by zkg algorithms.

#### Returns

Object - A DA object, or null when no DA was found:

- Sender: 32 Bytes - DA sender.
- Submmiter: 32 Bytes - broadcast DA data.
- Length: integer - DA data length.
- Index: integer - DA sender of index.
- Commitment: 48 Bytes - created by DA, we can match the commitment and DA by zkg algorithms.
- Data: N Bytes - DA data.
- Sign: N Bytes - signature.
- TxHash: 32 Bytes - txHash of L1 transaction.

### eth_batchFileDataByHashes

get a batch of DA data by a list of txHashs.

#### Parameters

object - A TxHashs obecjt

- TxHashes  Array: - a tx hash list;
-	BlockHash 	32 Bytes - The hash of a block.
-	BlockNumber  - integer of the number of block.

#### Returns

object - A return object:

- Flags  Array: - a DA data state Enumeration list.
    - DA data state Enumeration: DataState_SAVE,DataState_DEL,DataState_UNKNOW 
 
### eth_batchSaveFileDataWithHashes

save a batch of DA in disk by given txHashes.

#### Parameters

object - A TxHashs obecjt

- TxHashes  Array: - a tx hash list;
-	BlockHash 	32 Bytes - The hash of a block.
-	BlockNumber  - integer of the number of block.

#### Returns

Boolean - check node self have complete data or not.
Error - error message.

### eth_diskSaveFileDataWithHash

save a DA in disk by given txHash.

#### Parameters

hash 32 Bytes - The hash of a l1 transaction.

#### Returns
 
Boolean - check node self have complete data or not.
Error - error message.
  

