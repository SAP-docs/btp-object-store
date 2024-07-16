<!-- loio787fbe77f4eb46e0ae9a6222d57ba50e -->

# Object Versioning

Object versioning helps in keeping multiple versions of the same object. Versioning automatically maintains previous versions of an object.

When object versioning is enabled, you can restore an earlier version of an object to recover your data if it is erroneously modified or deleted. It can also be used to archive objects so that previous versions can be accessed. Overall, object versioning comes with an advantage of protecting end-users from the consequences of unintended overwrites and deletions. It can also be used to archive objects so that previous versions can be accessed. For more information on object versioning feature, see [AWS Documentation on Bucket Versioning](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Versioning.html).

*How to enable versioning? \(Recommended\)*

Versioning is enabled by default when a new instance is provisioned. Versioning configuration cannot be set to false - during `create-service` command. It can be updated any time later through the `update-service` command.

*How to disable versioning?*

Update the service instance with following command:

> ### Sample Code:  
> ```
> cf update-service <service_instance_name> -c '{"versioning" : false}'
> ```

The above commmand will disable the versioning of objects going forward. It must be noted that the existing versions of the objects created when versioning was enabled will continue to persist and hence be charged accordingly.

*How to re-enable versioning?*

Versioning can be re-enabled by updating an existing service instance with following command:

> ### Sample Code:  
> ```
> cf update-service <service_instance_name> -c '{"versioning" : true}'
> ```

*List of configuration parameters needed to configure versioning*


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

*How to get versioning status?*

> ### Sample Code:  
> ```
> cf serv ice <service_instance_name> --params
> ```

*Permissions*

On AWS based landscapes, below is the list of additional permissions given to a service binding user::

[Bucket Level](https://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html#using-with-s3-actions-related-to-bucket-subresources)

-   s3:ListBucketVersions


[Object level](https://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html#using-with-s3-actions-related-to-bucket-subresources)

-   s3:DeleteObjectVersion

-   s3:DeleteObjectVersionTagging

-   s3:GetObjectVersion

-   s3:GetObjectVersionAcl

-   s3:GetObjectVersionTagging

-   s3:GetObjectVersionTorrent

-   s3:PutObjectVersionAcl

-   s3:PutObjectVersionTagging


Object Store service would never suspend versioning on any S3 buckets owned by its customers. Rather, it provides option to consumers to change the configurations.

Once object versioning is enabled on a bucket, it will be applicable on all the objects residing in the bucket. Amazon doesn't provide a way to selectively enable the feature on a specific folder or an object.

> ### Note:  
> IMPACT ON THE COST
> 
> Please note that keeping a version of an object would be considered equivalent to storing a new object, from cost perspective. This implies that, for a given object, the total cost of storage would be equal to sum of storage cost of individual versions of the object. Therefore, it is recommended to carefully assess the storage cost aspects if you choose to keep versioning enabled.
> 
> Normal rates apply for every version of an object stored and transferred. Each version of an object is the entire object; it is not just a diff from the previous version. Thus, if you have three versions of an object stored, you are charged for three objects.

**Example on how to use object versioning feature**:

-   Adding objects to versioning-enabled buckets

    The examples for uploading objects in nonversioned and versioning-enabled buckets are the same, although in the case of versioning-enabled buckets, Amazon S3 assigns a version number. Otherwise, the version number is null. For more information, see [Adding objects to versioning-enabled buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/AddingObjectstoVersioningEnabledBuckets.html#add-obj-versioning-enabled-bucket-sdk).

-   Listing objects in versioning-enabled buckets

    The following example also work with a bucket that isn't versioning-enabled, or for objects that don't have individual versions. In those cases, Amazon S3 returns the object listing with a version ID of null.


> ### Sample Code:  
> ```
> // Retrieve the list of versions. If the bucket contains more versions
> // than the specified maximum number of results, Amazon S3 returns
> // one page of results per request.
> ListVersionsRequest request = new ListVersionsRequest().withBucketName(bucketName).withMaxResults(2);
> VersionListing versionListing = s3Client.listVersions(request);
> int numVersions = 0, numPages = 0;
> while (true) {
>   numPages++;
>   for (S3VersionSummary objectSummary : versionListing.getVersionSummaries()) {
>     System.out.printf("Retrieved object %s, version %s\n", objectSummary.getKey(), objectSummary.getVersionId());
>     numVersions++;
>   }
>   // Check whether there are more pages of versions to retrieve. If there are, retrieve them. Otherwise, exit the loop.
>   if (versionListing.isTruncated()) {
>     versionListing = s3Client.listNextBatchOfVersions(versionListing);
>   } else {
>     break;
>   }
> }
> ```

For more information, see [Listing objects in a versioning-enabled bucket](https://docs.aws.amazon.com/AmazonS3/latest/userguide/list-obj-version-enabled-bucket.html#list-obj-version-enabled-bucket-sdk-examples).

**How to retrieve or delete a specific version of an object?**

In the GET or DELETE request, please mention the version ID of the object that you would like to retrive or delete. For further details refer:

-   [Deleting object versions](https://docs.aws.amazon.com/AmazonS3/latest/dev/DeletingObjectVersions.html)
-   [Retrieving object versions](https://docs.aws.amazon.com/AmazonS3/latest/dev/RetrievingObjectVersions.html) 

**How to restore an earlier version of an object?**

-   In order to restore to the immediate previous version of an object, you may permanently delete the current version of the object.

-   In order to restore to an older version of an object, you can simply copy the previous version into the same bucket. The copied object would become the current version and all the earlier versions would remain preserved.

> ### Note:  
> Transitioning objects to a different storage class is not supported.

**Related Information**  


[Amazon S3 Object Versioning](https://docs.aws.amazon.com/AmazonS3/latest/dev/ObjectVersioning.html)

