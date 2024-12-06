<!-- loio4162969be1bd4b15987c0145fe8bcb6f -->

# Auto Expiration of Blobs and Blob Versions

You can set certain rules to delete objects when you want to avoid manual clean-up of objects or reduce storage cost.

> ### Note:  
> Object Store Service has done changes in the default configurations related to expiration of non-current versions of objects. For more information on the default settings on both new and existing instances, see [Default Configurations](default-configurations-152735d.md).



You can use the auto expiration capability, which allows you to use Lifecycle Management features on Azure landscapes. Apply multiple rules on a service instance with varying configurations to enable auto expiration for your storage account.



### Configuration

**Parameters**


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

array of expirationRule objects

</td>
<td valign="top">

yes

</td>
<td valign="top">

A list of expiration rules to be configured on a service instance. Must contain at least one expirationRule.

</td>
</tr>
</table>

**Expiration Rule Object**


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

name

</td>
<td valign="top">

string

</td>
<td valign="top">

yes

</td>
<td valign="top">

A rule name can have up to 256 alphanumeric characters. Rule name is case-sensitive and it must be unique.

</td>
</tr>
<tr>
<td valign="top">

disabled

</td>
<td valign="top">

boolean

</td>
<td valign="top">

no

</td>
<td valign="top">

Configure a rule to be temporary disabled. Defaults to false.

</td>
</tr>
<tr>
<td valign="top">

toBeDeleted

</td>
<td valign="top">

boolean

</td>
<td valign="top">

no

</td>
<td valign="top">

Configure a rule to be deleted. Defaults to false.

</td>
</tr>
<tr>
<td valign="top">

definitions\*

</td>
<td valign="top">

array of definition objects

</td>
<td valign="top">

no

</td>
<td valign="top">

A list of definitions for the expiration rule. Must contain at least one definition.

</td>
</tr>
<tr>
<td valign="top">

filters

</td>
<td valign="top">

array of filter objects

</td>
<td valign="top">

no

</td>
<td valign="top">

A list of filters for the expiration rule. Must contain at least one filter.

</td>
</tr>
</table>

\*Fields with an asterisk are required when toBeDeleted is undefined or false.

See the **How to configure auto expiration rules on Azure storage account?** section.

**Definition Object**


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

type

</td>
<td valign="top">

string

</td>
<td valign="top">

yes

</td>
<td valign="top">

Configure a rule to be applied on different types of objects. Supported types are base blob and version.

</td>
</tr>
<tr>
<td valign="top">

operator

</td>
<td valign="top">

string

</td>
<td valign="top">

yes

</td>
<td valign="top">

The condition for definition on current or previous versions of a blob. The supported operator is daysAfterModificationGreaterThan for type base blob and daysAfterCreationGreaterThan for type version.

</td>
</tr>
<tr>
<td valign="top">

value

</td>
<td valign="top">

number

</td>
<td valign="top">

yes

</td>
<td valign="top">

Indicates the time period in days.

</td>
</tr>
</table>

**Filter Object**


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

name

</td>
<td valign="top">

string

</td>
<td valign="top">

yes

</td>
<td valign="top">

The name of the filter. Current supported filter is `prefixMatch` and `blobIndexMatch`.

</td>
</tr>
<tr>
<td valign="top">

values

</td>
<td valign="top">

array of strings \(`prefixMatch`\)

</td>
<td valign="top">

yes

</td>
<td valign="top">

A list of strings for prefixes to be matched. Each rule can define up to 10 case-sensitive prefixes. A prefix string must start with a container name. For example, if you want to match all blobs under `https://myaccount.blob.core.windows.net/sample-container/blob1/...` for a rule, the values are \["sample-container/blob1"\]

</td>
</tr>
<tr>
<td valign="top">

 

</td>
<td valign="top">

array of tag elements \(`blobIndexMatch`\)

</td>
<td valign="top">

no

</td>
<td valign="top">

An array of dictionary values consisting of the blob index tag key and value conditions to be matched. Each rule can define up to 10 blob index tag conditions. For example, if you want to match all blobs with Project = Contoso under`https://myaccount.blob.core.windows.net/` for a rule, the `blobIndexMatch` is `{"name": "Project","op": "==","value": "Contoso"}`.

</td>
</tr>
</table>



### How to configure auto expiration rules on Azure storage account?

The default rules can be modified or new rules can be set through instance update operation.:

```
cf update-service <service_instance_name> -c sampleExpirationRules1.json
```

sampleExpirationRules1.json

```
{
    "autoExpiration": [
      {
        "name": "sample-rule1",
        "toBeDeleted": false,
        "disabled": true,
        "definitions": [
          {
            "type": "baseBlob",
            "operator": "daysAfterModificationGreaterThan",
            "value": "100.0"
          },
          {
            "type": "version",
            "operator": "daysAfterCreationGreaterThan",
            "value": "90.0"
          }
        ],
        "filters": [
          {
            "name": "prefixMatch",
            "values": [
              "sample-container/blob1",
              "sample-container/blob2"
            ]
          }
        ]
      },
      {
        "name": "sample-rule2",
        "disabled": false,
        "toBeDeleted": false,
        "definitions": [
          {
            "type": "version",
            "operator": "daysAfterCreationGreaterThan",
            "value": "90.0"
          }
        ],
        "filters": [
          {
            "name": "prefixMatch",
            "values": [
              "sample-container/blob3"
            ]
          }
        ]
      },
      {
  	"name": "sample-rule3",
  	"disabled": false,
  	"toBeDeleted": false,
  	"definitions": [
    	   {
      	      "type": "baseBlob",
              "operator": "daysAfterModificationGreaterThan",
              "value": "50.0"
    	   }
  	],
  	"filters": [
    	{
               "name": "prefixMatch",
      		"values": [
        	"sample-container1/blob4"
      		]
      	},
    	{
           "name": "blobIndexMatch",
      	   "values": [
              {
                  "name": "Project",
                  "op": "==",
                  "value": "Contoso"
              }
      	 ]
    	 }
       ]
     }
   ]
  }
```

The command enables three rules for your service instance:

-   sample-rule1 deletes base blobs after 100 days of no modification and versions after 90 days of creation on the objects with the prefix "sample-container/blob1" or "sample-container/blob2".
-   sample-rule2 deletes only noncurrent versions after 90 days of their creation on the objects with the prefix "sample-container/blob3".
-   sample-rule3 deletes baseBlobs after 50 days of no modification having the prefix "sample-container/blob3", blobIndex with "Project" as "Contoso".



### How to update an existing configured rule?

The following command changes the definitions in sample-rule2, which was configured earlier:

```
cf update-service <service_instance_name> -c sampleExpirationRules2.json
```

sampleExpirationRules2.json

```
{
    "autoExpiration": [
      {
        "name": "sample-rule2",
        "disabled": false,
        "toBeDeleted": false,
        "definitions": [
          {
            "type": "version",
            "operator": "daysAfterCreationGreaterThan",
            "value": "190.0"
          }
        ],
        "filters": [
          {
            "name": "prefixMatch",
            "values": [
              "sample-container/blob3"
            ]
          }
        ]
      }
    ]
 }
```



### How to delete existing configured rule? \(Method 1\) \(Recommended\)


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

The following will delete SampleRule1 and SampleRule2 if they exist in the bucket:

Example:

```
cf update-service <service_instance_name> -c SampleDeleteRule.json
```

SampleDeleteRule.json

```
{
    "deleteAutoExpiration": [
        "SampleRule1",
        "SampleRule2"
    ]
}
```

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



### How to delete an existing configured rule? \(Method 2\) \(Deprecated\)

The following command deletes sample-rule2:

```
cf update-service <service_instance_name> -c sampleExpirationRules3.json

```

sampleExpirationRules3.json

```
{
    "autoExpiration": [
      {
        "name": "sample-rule2",
        "toBeDeleted": true
      }
    ]
}
```



### How to retrieve the parameters configured on service instance?

The following command retrieves all the parameters prevent deletion, versioning, and auto expiration configured for a service instance:

```
cf service <service_instance_name> --params
```

Alternately, you can use the following command:

```
cf curl "/v2/service_instances/<service_instance_guid>/parameters"
```

The --params flag is only available cf8 onwards. If you're using an older version of cf and want to retrieve parameters, use the alternate command.

> ### Note:  
> -   Auto expiration rules can be configured on noncurrent versions of the object even though versioning is disabled. The rule can't be applied if there are no versions of the objects to be deleted.
> -   If you don't define prefixMatch or blobIndexMatch under filters, the rule applies to all blobs within the storage account.
> -   BlobIndexMatch can be used only with baseBlobs and not with version.
> -   If you set two rules, one deleting the base blob after 10 days as no modification and the other deleting base blob after 100 days of no modification. The base blob is deleted after 10 days of no modification.
> -   While updating a particular rule, the user needs to provide a complete updated rule and not just the part where modification is required. The rule is overridden with the latest configuration. Alternately, you can delete and create a fresh expiration rule.
> -   All the previously configured parameters stay as it is unless modified explicitly.
> -   Though auto expiration is an extension of [Lifecycle Management](https://docs.microsoft.com/en-us/azure/storage/blobs/lifecycle-management-overview), we don’t support tiering \(hot, cool, archive, and so on\) of blobs, selecting blob types & filtering based on blobIndexMatch.
> -   Transitioning objects to other storage classes isn't supported.

