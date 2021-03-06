# API Reference

## Lambda

### new Lambda(options)

Creates a new Lambda object.

| Param                   | Type     | Description       |
| ----------------------- | -------- | ----------------- |
| options                 | `Object` |                   |
| options.accessKeyId     | `String` | AWS access key ID |
| options.secretAccessKey | `String` | AWS secret key    |
| options.region          | `String` | AWS region        |

#### lambda.invoke(params, callback)

Invokes a Lambda function.

Request:

| Param                                                            | Type       | Description                                                                                                                                                                                                                                        |
| ---------------------------------------------------------------- | ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| params                                                           | `Object`   |                                                                                                                                                                                                                                                    |
| params.FunctionName <span style="color: red">**required**</span> | `String`   | The name of your lambda function                                                                                                                                                                                                                   |
| params.Payload                                                   | `String`   | The stringified JSON that you want to provide to your Lambda function as input                                                                                                                                                                     |
| params.InvocationType                                            | `String`   | How you would like to invoke your function. Options: <ul><li>`RequestResponse` **(default)** - Invoke lambda synchronously</li><li>`Event` - Invoke lambda asynchronously</li><li>`DryRun` - Validate parameters without invoking lambda</li></ul> |
| params.LogType                                                   | `String`   | Include details of the execution log in your response. Options: <ul><li>`None` - Don't supply any logs</li><li>`Tail` - Include logs</li></ul>                                                                                                     |
| params.ClientContext                                             | `String`   | Up to 3583 bytes of base64-encoded data about the invoking client to pass to the function in the context object                                                                                                                                    |
| params.Qualifier                                                 | `String`   | Specify a version or alias to invoke a published version of the function                                                                                                                                                                           |
| callback                                                         | `function` |                                                                                                                                                                                                                                                    |

Callback:

| Param                | Type      | Description                                                                                                                                                                                                                                                                                                                 |
| -------------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| err                  | `Error`   | The error object returned from the request. Set to `null` if the request is successful                                                                                                                                                                                                                                      |
| data                 | `Object`  | The data object returned from the request. Set to `null` if the request failed                                                                                                                                                                                                                                              |
| data.StatusCode      | `Integer` | The HTTP status code is in the 200 range for a successful request                                                                                                                                                                                                                                                           |
| data.FunctionError   | `String`  | If present, indicates that an error occurred during function execution. Options: <ul><li>`Handled` - The runtime caught an error thrown by the function and formatted it into a JSON document</li><li>`Unhandled` - The runtime didn't handle the error. For example, the function ran out of memory or timed out</li></ul> |
| data.LogResult       | `String`  | The last 4 KB of the execution log, which is base64 encoded                                                                                                                                                                                                                                                                 |
| data.Payload         | `Buffer`  | The response from the function, or an error object                                                                                                                                                                                                                                                                          |
| data.ExecutedVersion | `String`  | The version of the function that executed                                                                                                                                                                                                                                                                                   |

## STS

### new STS(options)

Creates a new STS object.

| Param                   | Type     | Description       |
| ----------------------- | -------- | ----------------- |
| options                 | `Object` |                   |
| options.accessKeyId     | `String` | AWS access key ID |
| options.secretAccessKey | `String` | AWS secret key    |
| options.region          | `String` | AWS region        |

#### sts.assumeRole(params, callback)

Request:

| Param                                                               | Type            | Description                                                                                                                                                                                                         |
| ------------------------------------------------------------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| params                                                              | `Object`        |                                                                                                                                                                                                                     |
| params.RoleArn <span style="color: red">**required**</span>         | `String`        | The Amazon Resource Name (ARN) of the role to assume                                                                                                                                                                |
| params.RoleSessionName <span style="color: red">**required**</span> | `String`        | An identifier for the assumed role session                                                                                                                                                                          |
| params.PolicyArns                                                   | `Array<map>`    | The Amazon Resource Names (ARNs) of the IAM managed policies that you want to use as managed session policies <br> Items are an `Object` with values `{ arn: String }`                                              |
| params.Policy                                                       | `String`        | An IAM policy in JSON format that you want to use as an inline session policy                                                                                                                                       |
| params.DurationSeconds                                              | `Integer`       | The duration, in seconds, of the role session                                                                                                                                                                       |
| params.Tags                                                         | `Array<map>`    | A list of session tags that you want to pass. Each session tag consists of a key name and an associated value <br> Items are an `Object` with values `{ key: String /* required */, value: String /* required */ }` |
| params.TransitiveTagKeys                                            | `Array<String>` | A list of keys for session tags that you want to set as transitive <br> Items are a `String`                                                                                                                        |
| params.ExternalId                                                   | `String`        | A unique identifier that might be required when you assume a role in another account                                                                                                                                |
| params.SerialNumber                                                 | `String`        | The identification number of the MFA device that is associated with the user who is making the `AssumeRole` call                                                                                                    |
| params.TokenCode                                                    | `String`        | The value provided by the MFA device                                                                                                                                                                                |

Callback:

| Param                              | Type      | Description                                                                                                                |
| ---------------------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------- |
| err                                | `Error`   | The error object returned from the request. Set to `null` if the request is successful                                     |
| data                               | `Object`  | The data object returned from the request. Set to `null` if the request failed                                             |
| data.Credentials                   | `map`     | The temporary security credentials, which include an access key ID, a secret access key, and a security (or session) token |
| data.Credentials.AccessKeyId       | `String`  | The access key ID that identifies the temporary security credentials                                                       |
| data.Credentials.SecretAccessKey   | `String`  | The secret access key that can be used to sign requests                                                                    |
| data.Credentials.SessionToken      | `String`  | The token that users must pass to the service API to use the temporary credentials                                         |
| data.Credentials.Expiration        | `Date`    | The date on which the current credentials expire                                                                           |
| data.AssumedRoleUser               | `map`     | The Amazon Resource Name (ARN) and the assumed role ID                                                                     |
| data.AssumedRoleUser.AssumedRoleId | `String`  | A unique identifier that contains the role ID and the role session name of the role that is being assumed                  |
| data.AssumedRoleUser.Arn           | `String`  | The ARN of the temporary security credentials that are returned from the `AssumeRole` action                               |
| data.PackedPolicySize              | `Integer` | A percentage value that indicates the packed size of the session policies and session tags combined passed in the request  |

## Kinesis

### new Kinesis(options)

Creates a new Kinesis object.

| Param                   | Type     | Description       |
| ----------------------- | -------- | ----------------- |
| options                 | `Object` |                   |
| options.accessKeyId     | `String` | AWS access key ID |
| options.secretAccessKey | `String` | AWS secret key    |
| options.region          | `String` | AWS region        |

#### kinesis.putRecords(params, callback)

Request:

| Param                                                                       | Type                                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| --------------------------------------------------------------------------- | ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| params                                                                      | `Object`                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| params.Records <span style="color: red">**required**</span>                 | `Array<map>`                        | The records associated with the request.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| params.Records[n].Data <span style="color: red">**required**</span>         | `Buffer, Typed Array, Blob, String` | The data blob to put into the record, which is base64-encoded when the blob is serialized. When the data blob (the payload before base64-encoding) is added to the partition key size, the total size must not exceed the maximum record size (1 MB).                                                                                                                                                                                                                                                                                                                                         |
| params.Records[n].ExplicitHashKey                                           | `String`                            | The hash value used to determine explicitly the shard that the data record is assigned to by overriding the partition key hash.                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| params.Records[n].PartitionKey <span style="color: red">**required**</span> | `String`                            | Determines which shard in the stream the data record is assigned to. Partition keys are Unicode strings with a maximum length limit of 256 characters for each key. Amazon Kinesis Data Streams uses the partition key as input to a hash function that maps the partition key and associated data to a specific shard. Specifically, an MD5 hash function is used to map partition keys to 128-bit integer values and to map associated data records to shards. As a result of this hashing mechanism, all data records with the same partition key map to the same shard within the stream. |
| params.StreamName <span style="color: red">**required**</span>              | `Array<map>`                        | The stream name associated with the request.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |

Callback:

| Param                          | Type         | Description                                                                                                                                                                                                                                                                                                              |
| ------------------------------ | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| err                            | `Error`      | The error object returned from the request. Set to `null` if the request is successful                                                                                                                                                                                                                                   |
| data                           | `Object`     | The data object returned from the request. Set to `null` if the request failed                                                                                                                                                                                                                                           |
| data.FailedRecordCount         | `Integer`    | The number of unsuccessfully processed records in a PutRecords request.                                                                                                                                                                                                                                                  |
| data.Records                   | `Array<map>` | An array of successfully and unsuccessfully processed record results, correlated with the request by natural ordering. A record that is successfully added to a stream includes SequenceNumber and ShardId in the result. A record that fails to be added to a stream includes ErrorCode and ErrorMessage in the result. |
| data.Records[n].SequenceNumber | `String`     | The sequence number for an individual record result.                                                                                                                                                                                                                                                                     |
| data.Records[n].ShardId        | `String`     | The shard ID for an individual record result.                                                                                                                                                                                                                                                                            |
| data.Records[n].ErrorCode      | `String`     | The error code for an individual record result. ErrorCodes can be either ProvisionedThroughputExceededException or InternalFailure.                                                                                                                                                                                      |
| data.Records[n].ErrorMessage   | `String`     | The error message for an individual record result. An ErrorCode value of ProvisionedThroughputExceededException has an error message that includes the account ID, stream name, and shard ID. An ErrorCode value of InternalFailure has the error message "Internal Service Failure".                                    |
| data.EncryptionType            | `String`     | The encryption type used on the records. Options: <ul><li>`NONE` - Do not encrypt the records.</li><li>`KMS` - Use server-side encryption on the records using a customer-managed AWS KMS key.</li></ul>                                                                                                                 |
