<!-- loiof99e2589472c44939a559d4b8f329a56 -->

# Object Versioning

Google Cloud Storage \(GCS\) offers object versioning to support the retrieval of objects that are deleted or replaced. You can enable or disable object versioning for your service instances \(buckets\).

**Configuration Parameters for GCS buckets**


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

enables or disables versioning for objects within a service instance

</td>
</tr>
</table>

**Enable Versioning for Objects in Cloud Storage Buckets**

Versioning is enabled by default. It can be modified through instance update operation:

```
cf update-service <service_instance_name> -c '{"versioning" : true}'
```

> ### Note:  
> Object Store Service has done changes in the default configurations related to versioning. For more information, see [Default Configurations](default-configurations-152735d.md). You can use the following commands based on your business scenario:

**Disable Versioning for Objects in Cloud Storage Buckets**

Update the service instance with following command:

```
cf update-service <service_instance_name> -c '{"versioning" : false}'
```

By doing this, you:

-   disable the versioning for objects. Existing versions of the objects created when versioning was enabled continue to persist and charged accordingly.


**Using Versioned Blobs through gsutil on gcloud**

After versioning is enabled:

-   Cloud Storage retains a non-current object version each time you replace or delete a live object version, as long as you do not specify the generation number of the live version.

-   Non-current versions retain the name of the object, but are uniquely identified by their generation number.

-   Non-current versions only appear in requests that explicitly call for them to be included.

-   You can permanently delete versions of objects by including the generation number in the deletion request or by using Object Lifecycle Management.


After versioning is disabled:

-   The bucket no longer accumulates new noncurrent versions of objects.

-   Object versions that already exist in the bucket are unaffected.


After versioning is enabled, you can see a list all the versions, restore older version, and several other version-specific operations with the help of gsutil commands. Also, you can restore an older version to be the live version when versioning is disabled. In this case, the prevailing live version is permenantly deleted and replaced by the restored copied version.

The following command lists all objects in the bucket including versions:

```
gsutil ls -r -a gs://<bucket_name>
```

The following command downloads a specific version of the object:

```
gsutil cp gs://<bucket_name>/<object_name>#<generation_number> SAVE_TO_LOCATION
```

Each object has a unique generation value. When you list all versions of the object, the response lists the versions including the geneation number.

The following command restores the live version of an object with a different version:

```
gsutil cp gs://<bucket_name>/<object_name>#<generation_number> gs://<bucket_name>/<object_name>
```

This operation creates a new object \(the contents of the -source-uri are copied into this new blob\). Consequently, there is an impact on the cost. To avoid this, delete the older version after restoring it to the current version.

The following command deletes an object version:

```
gsutil rm gs://<bucket_name>/<object_name>#<generation_number>
```

> ### Remember:  
> **Impact on Cost**
> 
> -   Keeping a version of a object is considered equivalent to storing a new object. This implies that, for a given object, the total cost of storage is equal to sum of storage cost for individual versions of the object. It is recommended that you assess the storage cost due to versioning.
> 
> -   Normal rates apply for each version of an object stored and transferred. Each version of a object is the entire object; it is not a different from the previous version. If you have three versions of an object stored, you are charged for all three objects.

**Related Information**  


[Google Cloud Storage Documentation: Object Versioning reference](https://cloud.google.com/storage/docs/object-versioning#reference)

[Prevent Accidental Deletion of GCS Buckets](https://help.sap.com/viewer/2ee77ef7ea4648f9ab2c54ee3aef0a29/Cloud/en-US/9164ace0159c46a2aee097c9d60a000e.html)

