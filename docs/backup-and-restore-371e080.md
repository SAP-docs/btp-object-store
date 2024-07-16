<!-- loio371e080d5a864abcb482b7ed2b3d9d30 -->

# Backup and Restore

Object Store service enables customers to use various supported hyperscalers' object store offerings. It enables only the features the underlying hyperscalers already support.

> ### Note:  
> There is no backup and restore feature provided by SAP Object Store service.

But, there are various features that are available that help in either preventing data loss or in restoring data back.

> ### Note:  
> We recommend you to go through the details of each of the supported features to have clarity about whether a feature is helpful in restoring data or preventing data deletion.



<a name="loio371e080d5a864abcb482b7ed2b3d9d30__section_axt_s4n_fyb"/>

## Data Replication across availability zones

In case of availability zone specific downtime/disasters, the respective hyperscalers are internally able to make the data available because each object is replicated across at least 3 availability zones in a specific region. Multi-AZ is enabled by default for all instances in all supported hyperscalers.

> ### Note:  
> Deviation: Instances on Azure created until Q2'21 are on single-AZ. We recommend migrating those to multi-AZ. For more information on how to migrate from single AZ to multi-AZ, see [Migrating Service Instances Created with LRS to ZRS](migrating-service-instances-created-with-lrs-to-zrs-29bd262.md).



<a name="loio371e080d5a864abcb482b7ed2b3d9d30__section_kxn_dpn_fyb"/>

## Restoring data after accidental deletion/modification

In case of accidental deletion or overwrites of objects, object versioning feature helps in restoring to the previous object versions. Versioning can be enabled on a bucket but it keeps multiple variants of an object in the same bucket. It can be used to preserve, retrieve, and restore every version of every object stored in a bucket. If versioning is enabled, then the deleted object version is preserved and can be restored, in case an object was deleted accidentally. Expiration rules can also be configured to delete older versions, to save storage cost.

For more information on the default configurations around versioning and expiration rules, see [Default Configurations](default-configurations-152735d.md).

For more information on versioning feature, refer the following links:

Object versioning on AWS, [Object Versioning](object-versioning-787fbe7.md) 

Object versioning on Azure, [Object Versioning](object-versioning-787fbe7.md)

Object versioning on GCP, [Object Versioning](object-versioning-f99e258.md)



<a name="loio371e080d5a864abcb482b7ed2b3d9d30__section_p5s_bqn_fyb"/>

## Preventing instance deletion

BTP Object Store Service supports the prevent instance deletion feature. If the preventDeletion is set to TRUE on an objectstore instance and if the corresponding bucket or container is not empty, then the service fails any instance deletion attempts. The flag needs to be set to FALSE or all the data within the bucket/container needs to be deleted, for the instance deletion operation to succeed.

To know more about the prevent instance deletion feature, please refer the following links:

AWS: [Prevent Accidental Deletion of AWS S3 Buckets](prevent-accidental-deletion-of-aws-s3-buckets-8c3c66d.md)

Azure: [Preventing Accidental Deletion of Azure Containers](preventing-accidental-deletion-of-azure-containers-67e5ba7.md)

GCP: [Prevent Accidental Deletion of GCS Buckets](prevent-accidental-deletion-of-gcs-buckets-9164ace.md)



<a name="loio371e080d5a864abcb482b7ed2b3d9d30__section_gsb_bym_vzb"/>

## Recover data after accidental instance deletion

In order to prevent permanent data loss due to an unintended instance deletion, Object Store Service has decoupled the deletion of resources from the deletion of corresponding instances. Even after an objectstore instance is deleted, the corresponding resource \(S3 bucket on AWS, storage container on Azure, GCS bucket on Google\) is retained until 14 days from the day of the instance deletion.



### How to restore the data after accidental deletion of an object store instance

-   A customer needs to create a ticket on ObjectStore, with the following details:

    -   Region
    -   Instance ID
    -   Timestamp of when the instance was deleted

-   If the ticket is created within the retention period, SAP support can create a technical user with read-only permissions and share credentials.
-   The customer also needs to create a new objectstore instance with a service key.
-   With read access to the soft-deleted bucket and write access to the new bucket, customer can copy data into the new bucket.
-   After complete data is copied successfully, customer can continue to use the service with the new instance.
-   Also, the customer needs to request deletion of the read-only technical user.
-   After the retention period is over, all the objects in the soft-deleted bucket will get deleted and finally the bucket will also get deleted.



### Additional points

-   BTP Object Store Service doesn't support the data migration itself. It has to be done by the customer only.
-   The amount of time it takes for all the data to get copied successfully, will depend upon the number of objects, the amount of storage and the mechanisms used for performing the data copy operations.
-   It is advised to start data migration as early as possible, so that there is enough time to copy everything before retention period is over.
-   1 way to copy the data is using an open source command line utility: rclone. Link:[https://rclone.org/s3/\#configuration](https://rclone.org/s3/#configuration). Please note that is open source and SAP doesn't own or provide any support with the same.
-   In case there is no need to restore data after an instance deletion, there is no action needed at the customer end. BTP Object Store Service handles the bucket deletion after the retention period is over.



### Impact on cost

Customers will not be charged after an instance is deleted. The cost during the retention period will be borne by the platform.

