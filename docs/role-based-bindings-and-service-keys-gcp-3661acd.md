<!-- loio3661acd901b6483096452fc24c29066a -->

# Role-Based Bindings and Service Keys \(GCP\)

Object Store supports creating service credentials with read and write roles. This allows applications to be bound to role-specific service bindings to restrict access per use case.

The role can be one of the following:

-   `read-only`: This role provides read-only access to the bucket.
-   `write-only`: This role provides write-only access to the bucket.

To get role-specific service credentials, an additional parameter must be passed during service key and binding creation. If the parameter is not passed, then it is considered to be the default case, in which all applicable permissions are given to the service credentials.



<a name="loio3661acd901b6483096452fc24c29066a__section_ewc_ww5_ncc"/>

## Permissions Associated with the `Read-Only` Role

-   The following permissions are granted when a service credential with `read-only` access is requested:
    -   resourcemanager.projects.get
    -   resourcemanager.projects.list
    -   storage.managedFolders.get
    -   storage.managedFolders.list
    -   storage.objects.get
    -   storage.objects.list




## Permissions Associated with the `Write-Only` Role

-   The following permissions are granted when a service credential with `write-only` access is requested:
    -   orgpolicy.policy.get
    -   resourcemanager.projects.get
    -   resourcemanager.projects.list
    -   storage.managedFolders.create
    -   storage.multipartUploads.abort
    -   storage.multipartUploads.create
    -   storage.multipartUploads.listParts
    -   storage.objects.create




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

The credentials structure will have an additional key with the name *role*, if the service binding or service key is created by passing a role.

```
  {
  "credentials": {
    "base64EncodedPrivateKeyData": "<base64_encoded_service_account_credentials>",
    "bucket": "<some_bucket_name>",
    "keyAlgo": "<service_account_key_generation_algo>",
    "projectId": "<project-id>",
    "region": "<region_of_bucket>",
    "role": "<role>"
  }
}
```

> ### Note:  
> -   The structure of the credentials does not change for the default bindings and service keys.
> -   Creating read-only or write-only service bindings and service keys is supported only for the standard plan. If you still have instances of the deprecated plans, then you would need to first update the instances to change the plan. See [Service Plan update to 'standard'](service-plan-update-to-standard-d891fb7.md).
> -   In GCP, some permissions are effective only when given together. Hence write-only binding will only be able to create objects and folders to a bucket.

