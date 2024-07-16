<!-- loio152735d289d6449f8da5639ab291f964 -->

# Default Configurations

BTP Object Store Service enables object versioning during objectstore instance provisioning, by default. In addition, it sets a default expiration rules, that allows deletion of non-current versions after 14 days.

The table below summarizes the default configurations followed at the time of instance creation, across all hyperscalers:


<table>
<tr>
<th valign="top">

 

</th>
<th valign="top">

Versioning

</th>
<th valign="top">

Expiration Rule

</th>
<th valign="top">

Prevent Instance Deletion

</th>
</tr>
<tr>
<td valign="top">

AWS

</td>
<td valign="top">

Enabled

</td>
<td valign="top">

Expire non-current versions after 14 days

</td>
<td valign="top">

False

</td>
</tr>
<tr>
<td valign="top">

Azure

</td>
<td valign="top">

Enabled

</td>
<td valign="top">

Expire non-current versions after 14 days

</td>
<td valign="top">

False

</td>
</tr>
<tr>
<td valign="top">

GCP

</td>
<td valign="top">

Enabled

</td>
<td valign="top">

Expire non-current versions after 14 days

</td>
<td valign="top">

False

</td>
</tr>
</table>

> ### Note:  
> Please refer the section below to know about the default configurations on older instances.

The default configurations could also be changed. To know more about how the versioning & object expiration configurations could be changed, please refer the following links:

Object versioning on AWS, [Object Versioning](object-versioning-787fbe7.md)

Object versioning on Azure, [Object Versioning](object-versioning-7c0f704.md)

Object versioning on GCP, [Object Versioning](object-versioning-f99e258.md)



<a name="loio152735d289d6449f8da5639ab291f964__section_uvp_b5n_fyb"/>

## Recommendations

We strongly recommend keeping both object versioning and preventDeletion enabled. This helps in preventing instance deletion by mistake and also help in restoring data to previous versions, if objects get deleted or modified accidentally. In case a use-case involves doing several overwrites, object expiration rules could also be used, to permanently delete the older versions after certain timeframe, to save on the storage cost.

> ### Caution:  
> If prevent deletion is not enabled, then the instance gets deleted, irrespective of whether object versioning was enabled or not.



<a name="loio152735d289d6449f8da5639ab291f964__section_dfh_p5n_fyb"/>

## Configurations on existing instances, created on or before July 27th, 2023

As versioning enablement is necessary to be able to restore data and prevent permanent data loss due to accidental deletion and overwrites, BTP Object Store Service has done the following configurations on all existing instances:

-   enabled object versioning, if it is found to be disabled.

-   set expiration rule to expire non-current versions of objects to expire after 14 days \(an object becomes non-current from the time it is overwritten and a new version becomes available\)
-   skip object versioning enablement, if the status is found to be 'suspended'

> ### Note:  
> After object versioning is enabled, it will start getting applied on all object uploads/overwrites from then onwards.


<table>
<tr>
<th valign="top">

 

</th>
<th valign="top">

Default configuration modification supported

</th>
<th valign="top">

Not supported

</th>
</tr>
<tr>
<td valign="top">

AWS - versioning and expiration rules

</td>
<td valign="top">

Yes through update-service operation

</td>
<td valign="top">

NA

</td>
</tr>
<tr>
<td valign="top">

Azure \(instances created Q3'21 onwards\)

</td>
<td valign="top">

Yes through update-service

</td>
<td valign="top">

 

</td>
</tr>
<tr>
<td valign="top">

Azure \(instances created until Q2'21\)

</td>
<td valign="top">

Yes \(via a ticket only\)

Supported at Cloud Foundry space level only.

All instances present in a single CF space are restricted to have a common configuration.

</td>
<td valign="top">

Different configurations on different instances part of the same CF space

</td>
</tr>
<tr>
<td valign="top">

GCP

</td>
<td valign="top">

Versioning can be modified through update-service operation.

For changes in expiration rules, a ticket needs to be created.

</td>
<td valign="top">

 

</td>
</tr>
</table>

> ### Note:  
> Possible cases during instance provisioning- During instance provisioning, passing versioning & expiration rules configurations is not supported. Object Store Service applies the default configuration, that could be changed later via update-service call.

