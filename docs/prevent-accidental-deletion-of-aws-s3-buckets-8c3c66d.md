<!-- loio8c3c66da50364e0bafb994f4c4b57042 -->

# Prevent Accidental Deletion of AWS S3 Buckets

On initiating service instance deletion call, Object Store service ensures deletion of service instance resources, which includes AWS S3 bucket\(s\), and hence the objects in the bucket also gets deleted.

In few instances, it is noted that the deletion was initiated and also approved \(in CLI/Cockpit\) accidentally, thereby deleting the objects and S3 bucket\(s\). Also, there are cases where you store important data in the AWS S3 Bucket and want to prevent accidental deletion of Object Store service instances.

To prevent this kind of accidental deletion of Object Store service instance, a new configuration parameter for service instance is introduced, which when set to true, will not initiate service instance deletion if there are objects/versions of object present in the S3 bucket.

To delete the service instance with Prevent Accidental Deletion feature set, you have to delete all the objects and object versions. After successful deletion of objects and their versions, delete service instance call works.

**Configuration Parameter**


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

preventDeletion

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Enables or disables deletion of buckets if objects are present

</td>
</tr>
</table>



<a name="loio8c3c66da50364e0bafb994f4c4b57042__section_x44_l55_kmb"/>

## Enable Prevent Accidental Deletion of AWS S3 Bucket feature

Create a service instance with following command:

```
cf create-service <service_name> <plan_name> <service_instance_name> -c '{"preventDeletion" : true}'
```

Alternatively, you can enable this feature by updating any existing service instance with the following command:

```
cf update-service <service_instance_name> -c '{"preventDeletion" : true}'
```

These commands:

-   Ensure the service instance of Object Store service is not deleted, if the AWS S3 Bucket has objects or object versions present.
-   Delete the service instance of Object Store service, if all the objects and object versions in AWS S3 bucket are deleted or if there is no objects or object versions present in S3 bucket.

> ### Note:  
> By default all service instances of Objectstore are not protected from accidental deletion, hence preventDeletion configuration is set to false by default. If users wish to protect their service instance from accidental deletion, preventDeletion configuration needs to be set to true - during `create-service` command or at any time later using `update-service` command.



<a name="loio8c3c66da50364e0bafb994f4c4b57042__section_rnd_y55_kmb"/>

## Disable Prevent Accidental Deletion of AWS S3 Bucket feature

Update the service instance with following command:

```
cf update-service <service_instance_name> -c '{"preventDeletion" : false}'
```

This command allows deletion of service instance of Object Store service, irrespective of objects and its versions present or not.

