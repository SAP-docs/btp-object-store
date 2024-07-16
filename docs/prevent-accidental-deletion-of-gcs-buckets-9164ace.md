<!-- loio9164ace0159c46a2aee097c9d60a000e -->

# Prevent Accidental Deletion of GCS Buckets

To prevent accidental deletion of Object Store service instance, a new configuration parameter for service instance is introduced, which when set, will not initiate service instance deletion if there are objects present in the bucket.

To delete the service instance with Prevent Accidental Deletion feature set, you have to delete all the objects. After successful deletion of objects, delete service instance call goes through.

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

Enables or disables deletion of buckets if objects are present.

</td>
</tr>
</table>



<a name="loio9164ace0159c46a2aee097c9d60a000e__section_x44_l55_kmb"/>

## Enable Prevent Accidental Deletion of GCS Bucket feature

Create a service instance with following command:

```
cf create-service <service_name> <plan_name> <service_instance_name> -c '{"preventDeletion" : true}'
```

Alternatively, you can enable this feature by updating any existing service instance with the following command:

```
cf update-service <service_instance_name> -c '{"preventDeletion" : true}'
```

This command:

-   Ensures the service instance of Object Store service is not deleted, if the GCS bucket has objects.
-   If all the objects are deleted or if there are no objects present in the bucket, this command will delete the service instance of Object Store service.

> ### Note:  
> By default all service instances of Objectstore are not protected from accidental deletion, hence preventDeletion configuration is set to false by default. If you want to protect the service instance from accidental deletion, set the preventDeletion configuration to true - during `create-service` command or at any time later using `update-service` command.



<a name="loio9164ace0159c46a2aee097c9d60a000e__section_rnd_y55_kmb"/>

## Disable Prevent Accidental Deletion of GCS bucket feature

Update the service instance with following command:

```
cf update-service <service_instance_name> -c '{"preventDeletion" : false}'
```

This command allows deletion of service instance of Object Store service, irrespective of objects are present in the bucket or not.

