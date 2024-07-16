<!-- loio67e5ba7dae7749c88483b8a3fe395eff -->

# Preventing Accidental Deletion of Azure Containers

To prevent accidental deletion of Object Store service instances, a new configuration parameter for service instance is introduced, which when set, will not initiate service instance deletion if there are objects present in the blob storage container.

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

Enables or disables deletion of containers if objects are present.

</td>
</tr>
</table>



<a name="loio67e5ba7dae7749c88483b8a3fe395eff__section_x44_l55_kmb"/>

## Enable Prevent Accidental Deletion of Azure blob storage container feature

Create a service instance with following command:

```
cf create-service <service_name> <plan_name> <service_instance_name> -c '{"preventDeletion" : true}'
```

Alternatively, you can enable this feature by updating any existing service instance with the following command:

```
cf update-service <service_instance_name> -c '{"preventDeletion" : true}'
```

This command:

-   Ensures the service instance of Object Store service is not deleted, if the Azure blob storage has objects or object versions present.
-   Deletes the service instance of Object Store service, if all the objects and object versions in Azure blob storage are deleted or if there is no objects or object versions present in container.

> ### Note:  
> By default all service instances of Objectstore are not protected from accidental deletion, hence preventDeletion configuration is set to false by default. If you want to protect the service instance from accidental deletion, set the preventDeletion configuration to true - during `create-service` command or at any time later using `update-service` command.



<a name="loio67e5ba7dae7749c88483b8a3fe395eff__section_rnd_y55_kmb"/>

## Disable Prevent Accidental Deletion of Azure blob storage container feature

Update the service instance with following command:

```
cf update-service <service_instance_name> -c '{"preventDeletion" : false}'
```

This command allows deletion of service instance of Object Store service, irrespective of objects and its versions present or not.

