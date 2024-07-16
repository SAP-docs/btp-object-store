<!-- loio7c0f704b5cc4408f9beae929c2f4bae5 -->

# Object Versioning

For instances created on the Zone Redundant Storage \(ZRS\) storage class, the Object Store service has a built-in capability that allows object \(blob\) versioning on Azure-based landscapes. Blob versioning is a feature provided by Azure.

Object versioning helps in maintaining multiple versions of the same object. For more information, see [Blob Versioning](https://docs.microsoft.com/en-us/azure/storage/blobs/versioning-overview).

Versioning maintains previous versions of a blob automatically. When blob versioning is enabled, you can restore an earlier version of a blob to recover your data if it was erroneously modified or deleted. It can also be used to archive blobs such that previous versions can be accessed.

**Configuration Parameters for Blob Versioning**


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

versioning

</td>
<td valign="top">

boolean

</td>
<td valign="top">

no

</td>
<td valign="top">

enables or disables versioning for blobs within a service instance

</td>
</tr>
</table>

**Enable Versioning for Azure Blobs**

Versioning is enabled by default when a new instance is provisioned. Versioning configuration cannot be set to false - during create-service command. It can be updated at any time later using update-service command.

> ### Note:  
> Object Store Service has done changes in the default configurations related to versioning. For more information on default settings on both new and existing instances, see [Default Configurations](default-configurations-152735d.md).

**Disable Versioning for Azure Blobs**

Update the service instance with following command:

```
cf update-service <service_instance_name> -c '{"versioning" : false}'
```

Then, you:

-   disable the versioning for blobs. Existing versions of the blobs created when versioning was enabled continue to persist and charged accordingly.

-   maintain the value of the preventDeletion config-parameter as it was during the previous create/update operation.


**Using Versioned Blobs through Azure Command-Line Interface \(CLI\)**

After versioning is enabled, you can see a list all the versions, restore an older version, and several other version-specific operations with the help of Az CLI commands.

The following command lists all blobs in the container including versions:

```
az storage blob list --account-name <storage_account> --container-name <container_name> --include v --sas-token sig="<sas_token>"

```

The following command downloads a specific version of the blob:

```
az storage blob download --account-name <storage_account> --container-name <container_name> --file ./local/download_to_this --name blob2download.txt --if-match <etag-value>  --sas-token sig="<sas_token>

```

Each blob has a unique e-tag value. When you list all blobs, the response contains properties of the blob including versionId, and e-tag value. versionId is the time-stamp at which the blob was modified or updated. Using the corresponding etag for the blob, you can download a specific version with the download command.

The following command restores a blob to a different version:

```
az storage blob copy start --account-name <storage_account> --destination-blob current.txt --destination-container <container_name> --source-uri "https://<storage_account>.blob.core.windows.net/<container_name>/current.txt?versionId=<version_id>&sig=<sas_token>" --sas-token "<sas_token>" 

```

This operation creates a new blob \(the contents of the -source-uri are copied into this new blob\). Consequently, there's an impact on the cost. To avoid it, delete the older version after restoring it to the current version.

The following command deletes a blob:

```
az storage blob delete --account-name <storage_account> --container-name <container_name> --name blob2delete.txt --if-match <etag-value>  --sas-token sig="<sas_token>

```

**Using REST APIs for Versioned Blobs**

The following request retrieves a list of all blobs in the container including all the versions:

```
GET https://<storage_account>.blob.core.windows.net/mycontainer?restype=<container_name>&comp=list&include=versions&<sas_token>

```

The SAS-Token appended at the end of the request must be URL-decoded.

> ### Remember:  
> **Impact on Cost**
> 
> -   Keeping a version of a blob is considered equivalent to storing a new blob. It implies that, for a given blob, the total cost of storage is equal to sum of storage cost for individual versions of the blob. It's recommended that you assess the storage cost if you wish to continue to have versioning enabled on your storage account.
> 
> -   Normal rates apply for each version of a blob stored and transferred. Each version of a blob is the entire object; it'sn't a different from the previous version. If you've three versions of an object stored, you're charged for all three objects.

**Related Information**  


[Preventing Accidental Deletion of Azure Containers](https://help.sap.com/viewer/2ee77ef7ea4648f9ab2c54ee3aef0a29/Cloud/en-US/67e5ba7dae7749c88483b8a3fe395eff.html)

[Migrating Service Instances Created with LRS to ZRS](https://help.sap.com/viewer/2ee77ef7ea4648f9ab2c54ee3aef0a29/Cloud/en-US/29bd26201a0c4d5c8cd922d3c0482677.html)

