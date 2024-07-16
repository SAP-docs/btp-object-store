<!-- loio52e2c18af86c45e2b1495cd594602304 -->

# Object Expiration Rules

Object Expiration allows you to schedule removal of your objects after a defined time period. It helps define rules to expire objects within a bucket based on which Amazon S3 deletes expired objects.

Object Store service allows you to use Amazon's Object Lifecycle Management feature for setting expiration rules for objects. To know more about expiration feature, please refer to Amazon's documentation on [Object Lifecycle Management](https://docs.aws.amazon.com/AmazonS3/latest/dev/object-lifecycle-mgmt.html).



*Default configurations*

A default expiration rule is set that ensures that all non-current versions are deleted after 14 days.

*How to modify default lifecycle configurations*

The default settings can be modified via instance update operation. It is advised to fetch the existing lifecycle rule using get-service operation and modify the same. Also, it is recommended to send the complete rule in the instance update operation.

*List of supported configuration parameters for modifying rules*


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Type

</th>
<th valign="top">

Mandatory

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

lifecycle Configuration

</td>
<td valign="top">

array of lifecycle configuration objects

</td>
<td valign="top">

yes

</td>
<td valign="top">

A list of rules to be configured on a service instance. Must contain at least one rule.

</td>
</tr>
</table>

LifecycleConfiguration object has the following parameters:


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Type

</th>
<th valign="top">

Mandatory

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

id

</td>
<td valign="top">

String

</td>
<td valign="top">

no

</td>
<td valign="top">

ID of the lifecycle rule configured for the storage space. Consists of at most 255 bytes. If not specified, or the value is empty, OSS will automatically generate a unique ID.

</td>
</tr>
<tr>
<td valign="top">

status

</td>
<td valign="top">

String

</td>
<td valign="top">

yes

</td>
<td valign="top">

Indicates the state the lifecycle rule is in. Value can be "Enabled" or "Disabled"\(by default\). If the rule is disabled, OSS will not perform any operations defined in the rule.

</td>
</tr>
<tr>
<td valign="top">

expirationInDays

</td>
<td valign="top">

Number

</td>
<td valign="top">

yes

</td>
<td valign="top">

Specify that the Object expires the storage type after N days of its last modification time.

</td>
</tr>
<tr>
<td valign="top">

expirationDate

</td>
<td valign="top">

Date

</td>
<td valign="top">

no

</td>
<td valign="top">

Specify an absolute date, and execute the expiration of storage type operation according to the Object whose last modification time is before this date.

</td>
</tr>
<tr>
<td valign="top">

filter

</td>
<td valign="top">

Object

</td>
<td valign="top">

yes

</td>
<td valign="top">

If specified, refers to the relative expiration time, indicating the retention period between the current version becoming a non-current version and the permanent deletion.

</td>
</tr>
<tr>
<td valign="top">

noncurrentVersionExpiration

</td>
<td valign="top">

Object

</td>
<td valign="top">

yes

</td>
<td valign="top">

If specified, refers to the relative expiration time, indicating the retention period between the current version becoming a non-current version and the permanent deletion.

</td>
</tr>
</table>

> ### Note:  
> A valid LifecycleConfiguration object must have either expirationInDays or noncurrentVersionExpiration, or both.

Filter object has two parameters: `predicate` and `and`.


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Type

</th>
<th valign="top">

Mandatory

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Predicate

</td>
<td valign="top">

Predicate object

</td>
<td valign="top">

no

</td>
<td valign="top">

Each S3 Lifecycle rule includes a filter that you can use to identify a subset of objects in your bucket to which the S3 Lifecycle rule applies

</td>
</tr>
<tr>
<td valign="top">

and

</td>
<td valign="top">

And object

</td>
<td valign="top">

no

</td>
<td valign="top">

Each S3 Lifecycle rule includes a filter that you can use to identify a subset of objects in your bucket to which the S3 Lifecycle rule applies

</td>
</tr>
</table>

Predicate object has the following parameters:


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Type

</th>
<th valign="top">

Mandatory

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

Prefix

</td>
<td valign="top">

String

</td>
<td valign="top">

no

</td>
<td valign="top">

The rule will be applied to the specified object that matches the prefix.

</td>
</tr>
<tr>
<td valign="top">

tag

</td>
<td valign="top">

Object

</td>
<td valign="top">

no

</td>
<td valign="top">

The rule will be applied to the objects that matches the tag value.

</td>
</tr>
</table>

And object has the following parameters:


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Type

</th>
<th valign="top">

Mandatory

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

prefix

</td>
<td valign="top">

String

</td>
<td valign="top">

no

</td>
<td valign="top">

The rule will be applied to the specified object that matches the prefix.

</td>
</tr>
<tr>
<td valign="top">

tags

</td>
<td valign="top">

Object

</td>
<td valign="top">

no

</td>
<td valign="top">

The rule will be applied to the objects that matches the tag value.

</td>
</tr>
</table>

> ### Note:  
> Filter object can have a predicate parameter or an and parameter.

Tag object has the following parameters:


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Type

</th>
<th valign="top">

Mandatory

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

key

</td>
<td valign="top">

String

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Key of the tag element

</td>
</tr>
<tr>
<td valign="top">

value

</td>
<td valign="top">

String

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Value of the tag element

</td>
</tr>
</table>

Tags object is a list and inside that it can have multiple key and value pairs.

NoncurrentVersionExpiration object has the following parameter:


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Type

</th>
<th valign="top">

Mandatory

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

days

</td>
<td valign="top">

Number

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Days after which the non-current object will be expired

</td>
</tr>
<tr>
<td valign="top">

newerNoncurrentVersions

</td>
<td valign="top">

Number

</td>
<td valign="top">

No

</td>
<td valign="top">

Number of non-current versions to retain

</td>
</tr>
</table>

Predicate: If the predicate parameter is used, then either the prefix or the tag can be specified, but not both. Refer to the example below.

Example with Prefix:

> ### Sample Code:  
> ```
> {
>   "autoExpiration": [
>     {
>       "id": "logs-rule",
>       "status": "Enabled",
>       "filter":{
>         "predicate":{
>             "prefix":"logs"
>          }
>       },
>       "expirationInDays": 90,
>       "expirationDate": null,
>       "noncurrentVersionExpiration": {
>         "days": 90,
>         "newerNoncurrentVersions": 1
>       },
>       "abortIncompleteMultipartUpload": null
>     }
>   ]
> }
> ```

Example with Tag:

> ### Sample Code:  
> ```
> {
>   "autoExpiration": [
>     {
>       "id": "logs-rule",
>       "status": "Enabled",
>       "filter":{
>         "predicate":{
>             "tag": {
>               "key": "key1",
>               "value": "value1"
>             }
>          }
>       },
>       "expirationInDays": 90,
>       "expirationDate": null,
>       "noncurrentVersionExpiration": {
>         "days": 90,
>         "newerNoncurrentVersions": 1
>       },
>       "abortIncompleteMultipartUpload": null
>     }
>   ]
> }
> ```

> ### Note:  
> Do not use both a prefix and a tag together inside a predicate as it may cause unexpected behaviour.

And: If the and parameter is used, then at most one prefix and any number of tags can be specified. Refer to the example below.

> ### Sample Code:  
> ```
> {
>   "autoExpiration": [
>     {
>       "id": "logs-rule",
>       "status": "Enabled",
>       "filter":{
>         "and": {
>           "prefix": "logs",
>           "tags": [
>             {
>               "key": "key1",
>               "value": "value1"
>             },
>             {
>               "key": "key1",
>               "value": "value1"
>             }
>           ]
>         }
>       },
>       "expirationInDays": 90,
>       "expirationDate": null,
>       "noncurrentVersionExpiration": {
>         "days": 90,
>         "newerNoncurrentVersions": 1
>       },
>       "abortIncompleteMultipartUpload": null
>     }
>   ]
> }
> ```

Example:

> ### Sample Code:  
> ```
> cf update-service <service_instance_name> -c SampleRule.json
> ```

SampleRule.json

> ### Sample Code:  
> ```
> {
>   "autoExpiration": [
>     {
>       "id": "SampleRule1",
>       "status": "Enabled",
>       "filter":{
>         "predicate":{
>             "prefix":"test/"
>          }
>       },
>       "expirationInDays": 90,
>       "expirationDate": null,
>       "noncurrentVersionExpiration": {
>         "days": 90,
>         "newerNoncurrentVersions": 1
>       },
>       "abortIncompleteMultipartUpload": null
>     }
>   ]
> }
> ```

*How to get existing lifecycle rule?*

> ### Sample Code:  
> ```
> cf service <service_instance_name> --params
> ```

*List of supported configuration parameters*


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Type

</th>
<th valign="top">

Mandatory

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

autoExpiration

</td>
<td valign="top">

Array of Rule Objects

</td>
<td valign="top">

no

</td>
<td valign="top">

Existing rule set on the bucket

</td>
</tr>
</table>



### Deleting configured Lifecycle rules

Objectstore Service now allows deleting Lifecycle rules that have been configured using Amazon's Object Lifecycle Management.

SUPPORTED CONFIGURATION PARAMETERS


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Type

</th>
<th valign="top">

Mandatory

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

deleteAutoExpiration

</td>
<td valign="top">

String Array of Rule Ids

</td>
<td valign="top">

yes

</td>
<td valign="top">

Existing rules set on the bucket

</td>
</tr>
</table>

Example:

> ### Sample Code:  
> ```
> cf update-service <service_instance_name> -c SampleDeleteRule.json
> ```

SampleDeleteRule.json

> ### Sample Code:  
> ```
> {
>     "deleteAutoExpiration": [
>         "SampleRule1",
>         "SampleRule2"
>     ]
> }
> ```

> ### Note:  
> -   Do not pass any other parameter in the update call along with `deleteAutoExpiration`, as we do not allow any other operation along with this.
> -   It is advised to fetch the existing lifecycle rule\(s\) using get-service operation and then provide us with the latest rule id\(s\) that are to be deleted in the above format.
> -   If any of the rule id\(s\) provided do not exist in the bucket, then the request will fail with the following error:
> 
>     ```
>     Following rule identifiers passed: [SampleRule3, SampleRule4] is/are incorrect. Please do the instance GET operation to fetch the existing rule identifiers.
>     ```
> 
> -   If deleting a lifecycle rule is attempted when there are no rules present in the bucket, the request will fail with the following error:
> 
>     ```
>     No Existing lifecycle configurations present in IaaS to delete.
>     ```

> ### Note:  
> -   Transitioning objects to other storage classes is not supported\*.
> 
> -   Object Store service does not support transitioning objects to other storage classes \(other than Standard storage class\). Even though it is technically still possible to set transition rules, we highly discourage you to set such rules.
> -   If objects are transitioned to other storage classes, users will not be able to retrieve those back.
> -   Also, if objects are transitioned to other storage classes by setting transition rules, the storage cost will not be reduced from what is charged for standard storage class currently.

