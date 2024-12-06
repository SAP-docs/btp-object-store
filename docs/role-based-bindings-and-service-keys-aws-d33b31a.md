<!-- loiod33b31aec6864e3184b7ebcefb322149 -->

# Role-Based Bindings and Service Keys \(AWS\)

Object Store supports creating service credentials with read and write roles. This allows applications to be bound to role-specific service bindings to restrict access per use case.

The role can be one of the following:

-   `read-only`: This role provides read-only access to the bucket.
-   `write-only`: This role provides write-only access to the bucket.

To get role-specific service credentials, an additional parameter must be passed during service key and binding creation. If the parameter is not passed, then it is considered to be the default case, in which all applicable permissions are given to the service credentials.



<a name="loiod33b31aec6864e3184b7ebcefb322149__section_ewc_ww5_ncc"/>

## Permissions Associated with the `Read-Only` Role

-   The following permissions are granted to a bucket when a service credential with `read-only` access is requested:
    -   ListBucket
    -   ListBucketMultipartUploads
    -   GetBucketLocation
    -   ListBucketVersions
    -   GetBucketLogging \(Only when server access logging is enabled. See [Server Access Logging](server-access-logging-b03c5b9.md).\)

-   The following permissions are granted to an object when a service credential with `read-only` access is requested:
    -   GetObject
    -   GetObjectAcl
    -   GetObjectTorrent
    -   GetObjectTagging
    -   GetObjectVersion
    -   GetObjectVersionAcl
    -   GetObjectVersionTagging
    -   GetObjectVersionTorrent
    -   ListMultipartUploadParts




## Permissions Associated with the `Write-Only` Role

-   No permissions are granted to a bucket when a service credential with `write-only` access is requested.
-   The following permissions are granted to an object when a service credential with `write-only` access is requested:
    -   AbortMultipartUpload
    -   DeleteObject
    -   DeleteObjectTagging
    -   DeleteObjectVersion
    -   DeleteObjectVersionTagging
    -   PutObject
    -   PutObjectAcl
    -   PutObjectTagging
    -   PutObjectVersionTagging
    -   PutObjectVersionAcl




## Configuration Parameters to Get Role-Based Service Credentials


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

role

</td>
<td valign="top">

string

</td>
<td valign="top">

no

</td>
<td valign="top">

to create a role-based binding

</td>
</tr>
</table>



## Values Associated with the Role Parameter


<table>
<tr>
<th valign="top">

Value

</th>
<th valign="top">

Type

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

read

</td>
<td valign="top">

string

</td>
<td valign="top">

to create a read-based role binding

</td>
</tr>
<tr>
<td valign="top">

write

</td>
<td valign="top">

string

</td>
<td valign="top">

to create a write-based role binding

</td>
</tr>
</table>



## Examples

-   Read-only role:

    ```
    cf create-service-key <serviceInstanceName> <keyName> -c '{"role": "read"}'
    ```

-   Write-only role:

    ```
    cf create-service-key <serviceInstanceName> <keyName> -c '{"role": "write"}'
    ```




## Additional Parameter in `credentials`

An extra parameter is added with the key `role` in the credentials section of the service key in case of role-based binding or service key. The value of the role parameter will be either `read` or `write` based on the role requested.

```
 "credentials": {  
    "access_key_id": "<some_access_key_id>",  
    "bucket": "<some_bucket_name>",  
    "role": "<role>",
    "host": "<region_specific_s3_endpoint>",
    "region": "<region>",  
    "secret_access_key": "<some_secret_access_key>",  
    "uri": "s3://<some_access_key_id>:<some_secret_access_key>@<region_specific_s3_endpoint>/<some_bucket_name>",  
    "username": "<some_username>"  
  }
```

> ### Note:  
> -   The structure of the credentials does not change for the default bindings and service keys.
> -   Creating read-only or write-only service bindings and service keys is supported only for the standard plan. If you still have instances of the deprecated plans, then you would need to first update the instances to change the plan. See [Service Plan update to 'standard'](service-plan-update-to-standard-d891fb7.md).

