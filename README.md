﻿# Weave-Commons

[![Build status](https://ci.appveyor.com/api/projects/status/p87ij8921enurk50/branch/master?svg=true)](https://ci.appveyor.com/project/bazzilic/weave-commons/branch/master)

The `Weave.Commons` project contains basic models for WEAVE, as well as the plugin interface to process datasets in the authority node.

## IWeaveDatasetPlugin

The `IWeaveDatasetPlugin` interface defines the following methods:

### `LoadConfig(IConfiguration configuration)`

This method receives all configuration parameters, and is called on WEAVE authority node startup.

### `DatasetReady(Dataset dataset)`

This method receives a submitted dataset, and is called whenever a dataset is ready (tokenized and joined).

### `UpdateDatasets(byte[] updateKey, byte[] publicKey)`

This method gets an update key and public key, to update all datasets in your own data store. It is called whenever datasets needs to be updated due to key changes.

The `updateKey` and `publicKey` parameters are `BigInteger` values represented by an byte array. To get the new token, the equation is represented by: `newToken = (oldToken^updateKey) mod publicKey`.

#### Usage Example

```csharp
public void UpdateDatasets(byte[] updateKey, byte[] publicKey)
{
    var newToken = BigInteger.ModPow(new BigInteger(oldValue), new BigInteger(SecretKey), new BigInteger(PublicKey));
}
```