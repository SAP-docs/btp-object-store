<!-- loio8be157a916d943118200c3675bacde84 -->

# Role-Based Bindings and Service Keys \(Azure\)

Object Store supports creating service credentials with read and write roles. This allows applications to be bound to role-specific service bindings to restrict access per use case.

The role can be one of the following:

-   `read-only`: This role provides read-only access to the container.
-   `write-only`: This role provides write-only access to the container.

To get role-specific service credentials, an additional parameter must be passed during service-key and binding creation. If the parameter is not passed, then it is considered to be the default case, in which all applicable permissions are given to the service credentials.



## Permissions Associated with the `Read-Only` Role

The following permissions are granted to a container when a service credential with `read-only` access is requested:

-   Read: Permission to read the content, properties, metadata, and block list of a blob.
-   List: Permission to list blobs in a container.
-   Filter: Permission to read and filter by blob tags.



## Permissions Associated with the `Write-Only` Role

The following permissions are granted to a container when a service credential with `write-only` access is requested:

-   Add: Permission to add a block to an append blob.
-   Create: Permission to write a new blob or copy a blob to a new blob.
-   Write: Permission to create or write content, properties, metadata, and block list of a blob.
-   Delete: Permission to delete a blob.
-   Delete version: Permission to delete a blob version.
-   Permanent delete: Permission to permanently delete a blob or blob version.
-   Tag: Permission to read or write blob tags.
-   Move: Permission to move a blob \(only applicable in certain scenarios\).
-   Execute: Permission to execute a blob query \(not commonly used\).
-   Set immutability policy: Permission to set an immutability policy on a blob.



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

The credentials structure has an additional key with the name *role* if the service binding or service key is created by passing a role.

```
{
  "credentials": {
    "account_name": <account_name>,
    "container_name": <container_name>,
    "container_uri": <container_uri>,
    "region": "<region>",
    "role": "read",
    "sas_token": <sas>
  }
}
```

> ### Note:  
> -   The structure of the credentials does not change for the default bindings and service keys.
> -   Creating read-only or write-only service bindings and service keys is supported only for the standard plan. If you still have instances of the deprecated plans, then you would need to first update the instances to change the plan. See [Service Plan update to 'standard'](service-plan-update-to-standard-d891fb7.md).
> -   Azure does not support separate permissions for reading and writing blobs tags. Hence it is kept under the write role.

