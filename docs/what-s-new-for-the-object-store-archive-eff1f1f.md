<!-- loioeff1f1f401a24f4fa117909ed0fb348e -->

# What's New for the Object Store \(Archive\)





****


<table>
<tr>
<th valign="top">

Technical Component

</th>
<th valign="top">

Environment

</th>
<th valign="top">

Title

</th>
<th valign="top">

Description

</th>
<th valign="top">

Action

</th>
<th valign="top">

Lifecycle

</th>
<th valign="top">

Type

</th>
<th valign="top">

Line of Business

</th>
<th valign="top">

Modular Business Process

</th>
<th valign="top">

Product

</th>
<th valign="top">

Latest Revision

</th>
<th valign="top">

Available as of

</th>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

AWS: S3 specific permissions for versioning & expiration rules configurations to be revoked.

</td>
<td valign="top">

AWS S3 permissions: *GetBucketVersioning*, *PutBucketVersioning*, *PutLifecycleConfiguration* and *GetLifecycleConfiguration* are deprecated since 2023-09-07 and will be revoked after 2024-01-09.

Action: To continue to use these capabilities, switch to alternate approach involving instance update. See [Object Versioning](object-versioning-787fbe7.md) & [Object Expiration Rules](object-expiration-rules-52e2c18.md) for details.

</td>
<td valign="top">

Required

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

Announcement

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2023-11-16

</td>
<td valign="top">

2023-11-16

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Modification to versioning & expiration rules configurations allowed only through instance update operation

</td>
<td valign="top">

On all 3 supported hyperscalers, default configurations will continue to be applied during instance creation. Any changes to those will be possible only through instance update operation.

Action: See, Azure, [Object Versioning](object-versioning-7c0f704.md)

AWS, [Object Versioning](object-versioning-787fbe7.md)

GCP, [Object Versioning](object-versioning-f99e258.md)

</td>
<td valign="top">

Required

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2023-10-19

</td>
<td valign="top">

2023-10-19

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

The new “Standard” service plan is now available for Object Store on SAP BTP, this new service plan unifies the delivery of the service in all hyperscalers, simplifying the existing commercial plans.

</td>
<td valign="top">

The standard plan is the replacement of the existing Azure, AWS and GCP specific service plans \("azure-standard", "s3-standard" and "gcs-standard"\). For more information, please see [Service Plans and Entitlements](service-plans-and-entitlements-26c3918.md) and [Service Plan update to 'standard'](service-plan-update-to-standard-d891fb7.md) sections.

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2023-07-01

</td>
<td valign="top">

2023-07-01

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

AWS: Deprecation of GetBucketVersioning and PutBucketVersioning

</td>
<td valign="top">

The permissions to directly enable, disable and get versioning on a bucket are deprecated and will be removed in future.

Action: See [Object Versioning](object-versioning-787fbe7.md).

</td>
<td valign="top">

Required

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2023-09-07

</td>
<td valign="top">

2023-09-07

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

AWS: configure versioning through instance update

</td>
<td valign="top">

Versioning configuration now supported through instance update call.

Action: See [Object Versioning](object-versioning-787fbe7.md).

</td>
<td valign="top">

Required

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2023-09-07

</td>
<td valign="top">

2023-09-07

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

GCP – Change in default configuration

</td>
<td valign="top">

Enablement of Object Versioning on all existing and new instances.

Action: See [Object Versioning](object-versioning-787fbe7.md).

</td>
<td valign="top">

Required

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2023-08-04

</td>
<td valign="top">

2023-08-04

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

AWS – Change in default configuration

</td>
<td valign="top">

Enablement of Object Versioning on all existing and new instances.

Action: See [Backup and Restore](backup-and-restore-371e080.md).

</td>
<td valign="top">

Required

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2023-07-28

</td>
<td valign="top">

2023-07-28

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Azure – Change in default configuration

</td>
<td valign="top">

Enablement of Object Versioning on all existing and new instances.

Action: See [Backup and Restore](backup-and-restore-371e080.md).

</td>
<td valign="top">

Required

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2023-07-28

</td>
<td valign="top">

2023-07-28

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Azure – Support object level tagging

</td>
<td valign="top">

You can now set and retrieve tags on blobs

Action: See [Object Level Tagging](https://help.sap.com/docs/object-store/object-store-service-on-sap-btp/object-level-tagging).

</td>
<td valign="top">

Recommended

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2023-06-15

</td>
<td valign="top">

2023-06-15

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Azure - Change in blob endpoint URL

</td>
<td valign="top">

Blob endpoint URL, part of ‘container\_uri’, will change. Please plan to assess any impact and adapt, if required.

Action: See [Change in Blob Endpoint URL: Assess and Adapt](https://help.sap.com/docs/object-store/object-store-service-on-sap-btp/change-in-blob-endpoint-url-assess-and-adapt) 

</td>
<td valign="top">

Required

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">

2023-04-06

</td>
<td valign="top">

2023-04-06

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Get parameters configured on service instances created on AWS, Azure and GCP

</td>
<td valign="top">

Get view of a successfully provisioned instance using the instance retrievable capability, to know about related configurations.

Action: See [Retrieve Parameters Configured on Service Instance](https://help.sap.com/docs/ObjectStore/2ee77ef7ea4648f9ab2c54ee3aef0a29/8b617c6ba2ba4660bd488927a64ffdfb.html) 

</td>
<td valign="top">

Recommended

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2022-11-08

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Adoption: Consumers of gcs-standard plan

</td>
<td valign="top">

Lifecycle operations: create-service, delete-service, and update-service would be made asynchronous in all GCP based regions.

Please plan to test your deployment scripts with respect to asynchronous behaviour of the three operations and plan to adapt if required.

Action: See [Configure Object Store to use GCP](https://help.sap.com/docs/ObjectStore/2ee77ef7ea4648f9ab2c54ee3aef0a29/687cd27b9383425fb0f64e9b0ea53a2c.html?locale=en-US) 

</td>
<td valign="top">

Required

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

Announcement

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2022-09-08

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Support for auto expiration of blobs and blob versions on Azure

</td>
<td valign="top">

You can now set rules to delete blobs and blob versions automatically. See, [Auto Expiration of Blobs and Blob Versions .](https://help.sap.com/docs/ObjectStore/2ee77ef7ea4648f9ab2c54ee3aef0a29/4162969be1bd4b15987c0145fe8bcb6f.html?locale=en-US) 

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2022-06-07

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Support for Object Versioning on GCP

</td>
<td valign="top">

The service supports object versioning for service instances on GCP in the Cloud Foundry environment. See [GCP: Object Versioning](https://help.sap.com/viewer/2ee77ef7ea4648f9ab2c54ee3aef0a29/Cloud/en-US/f99e2589472c44939a559d4b8f329a56.html).

Action: Enable or disable object versioning for your service instances based on your business use case.

</td>
<td valign="top">

Recommended

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2022-05-05

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

Support for Object Versioning on Azure

</td>
<td valign="top">

The service supports object versioning for service instances on Azure in the Cloud Foundry environment and Kyma environment. See [Azure Blob Storage: Object Versioning](https://help.sap.com/viewer/2ee77ef7ea4648f9ab2c54ee3aef0a29/Cloud/en-US/7c0f704b5cc4408f9beae929c2f4bae5.html).

Action: Enable or disable object versioning for your service instances based on your business use case.

</td>
<td valign="top">

Recommended

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2022-05-05

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

For users of Object Store Service on Azure

</td>
<td valign="top">

It has been identified that incorrect data can get uploaded during retries while using Blob SDK: 12.0 – 12.6.1 versions. This has been fixed with newer releases by Microsoft. Please update to 12.13 or later, if you are affected.

</td>
<td valign="top">

Required

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2021-09-24

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

For the users of Object Store service on Azure based landscapes

</td>
<td valign="top">

Migration steps are now available that you should follow to move existing instances \(created before Q2 2021\) from LRS \(Single AZ\) to ZRS \(Multi-AZ\). See, [Migrating Service Instances Created with LRS to ZRS](migrating-service-instances-created-with-lrs-to-zrs-29bd262.md) 

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2021-09-13

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry

-   Kyma



</td>
<td valign="top">

For the users of Object Store service on AWS based landscapes

</td>
<td valign="top">

All object/bucket operations with TLS version lower than 1.2 would be denied as of September 13'th 2021.

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2021-08-27

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

For the users of Object Store service on Azure based landscapes

</td>
<td valign="top">

As part of BTP’s goal to enable Multi-AZ for all services, Object Store Service would start supporting Zone Redundant Storage \(ZRS\) on Azure for new instances of the service. See, [Service Plans and Entitlements](service-plans-and-entitlements-26c3918.md).

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2021-07-01

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Kyma



</td>
<td valign="top">

Consume AWS specific plans from Kyma environment

</td>
<td valign="top">

The service supports consumption of AWS specific plans from Kyma environment, in addition to the Cloud Foundry environment. See, [Consumption in the Kyma Environment](consumption-in-the-kyma-environment-11f50ef.md).

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2021-06-17

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

For the users of Object Store service on AWS based landscapes

</td>
<td valign="top">

We've enabled "secure transfer" in all the S3 buckets \(existing and new ones\). Hence, you need to make all the operations on S3 buckets over HTTPS only. No HTTP calls will be allowed.

</td>
<td valign="top">

Required

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2021-04-22

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

For the users of Object Store service on AWS based landscapes

</td>
<td valign="top">

Object Store service will apply bucket policy to deny any actions without “Secure Transport” enabled on both existing and new S3 buckets. We recommend making all the operations on the bucket and objects within the HTTPS, to avoid any disruptions. If you are already making all the calls to your bucket over HTTPS, then there is no action required from your side.

Timelines:

From March 29'th, 2021: The bucket policy will be applied to new S3 buckets that get created.

April 22'nd, 2021: The policy will be applied to all the buckets created before March 29th.

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2021-03-11

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Plan for Adaption: users of s3- standard plans

</td>
<td valign="top">

The `create-service`, `delete-service` and `update-service` operations are now asynchronous for all the plans offered by the service on AWS. You need not retry if there are multiple concurrent instance creation requests. See, [Configure Object Store to use Amazon Simple Storage Service](configure-object-store-to-use-amazon-simple-storage-service-4236b94.md).

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2021-02-25

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Consume Azure specific plans from Kyma environment

</td>
<td valign="top">

The service supports consumption of Azure specific plans from Kyma environment, in addition to the Cloud Foundry environment. See, [Consumption in the Kyma Environment](consumption-in-the-kyma-environment-9bbfed9.md).

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2021-02-25

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Plan for Adaption: users of s3- standard plans

</td>
<td valign="top">

We are enhancing the Object Store service to make the`create-service`, `delete-service`, and`update-service` calls asynchronous.

This announcement is a heads-up for the consumers of the s3-standard service plan to plan adaption for these operations.

We plan to release the enhancement in AWS based live landscape on February 25th.

We'll provide more detailed documentation at the time of release.

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2021-01-19

</td>
</tr>
<tr>
<td valign="top">

Object Store

</td>
<td valign="top">

-   Cloud Foundry



</td>
<td valign="top">

Prevent Accidental Deletion of GCS Buckets

</td>
<td valign="top">

You can now prevent accidental deletion of ‘objectstore’ instances with ‘gcs-standard’ plan, in case of non-empty GCS buckets. See, [Prevent Accidental Deletion of GCS Buckets](prevent-accidental-deletion-of-gcs-buckets-9164ace.md).

</td>
<td valign="top">

Info only

</td>
<td valign="top">

General Availability

</td>
<td valign="top">

New

</td>
<td valign="top">

Technology

</td>
<td valign="top">

Not applicable

</td>
<td valign="top">

 

</td>
<td valign="top">



</td>
<td valign="top">

2021-01-14

</td>
</tr>
</table>

