<!-- loioa37de846c05a49d9b74a9acc5d35901b -->

# Enable Continuous Backup

Enable continuous backups of an Amazon S3 bucket to safeguard data from accidental deletion of objects. With continuous backups enabled, a backup job runs daily and creates a recovery point for restoration.



<a name="loioa37de846c05a49d9b74a9acc5d35901b__prereq_mcd_4ks_pcc"/>

## Prerequisites

-   The Object Store instance must be the `standard` plan. Continuous backups are not supported for the `s3-standard` plan, which was deprecated in Q4 2023. For more information, see [Service Plan update to 'standard'](service-plan-update-to-standard-d891fb7.md).
-   Versioning must be enabled on the instance before enabling continuous backup. If versioning is disabled, AWS will not allow configuring continuous backup.

> ### Restriction:  
> -   Once continuous backups are enabled, they cannot be disabled. You can, however, change the retention period.
> -   During an instance update operation, you cannot set any other configuration parameters while enabling continuous backups or setting the retention period.



## Context

Continuous backup is disabled by default.

Continuous backup will take up to 2 hours to get started. Time taken to finish the first backup depends upon the amount of data in terms of number of objects and the size of objects.

> ### Note:  
> When an `objectstore` instance is deleted, continuous backups are disabled and existing backups are deleted. The Amazon S3 bucket with the existing data is retained for a period of 14 days; see [Backup and Restore](backup-and-restore-371e080.md).

Continuous backups come with additional cost. There will be increased storage cost due to the backup-related storage. This will be reflected in the existing `storage_in_GB` metric.



## Procedure

Enable backups using the `create-service` call or later using the `update-service` call:

```
cf create-service <service_instance_name> -c '{"backupEnabled":true,"backupRetentionPeriod":<n>}'
```

```
cf update-service <service_instance_name> -c '{"backupEnabled":true,"backupRetentionPeriod":<n>}'
```

**Configuration Parameters**


<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Type

</th>
<th valign="top">

Required

</th>
<th valign="top">

Description

</th>
</tr>
<tr>
<td valign="top">

backupEnabled

</td>
<td valign="top">

boolean

</td>
<td valign="top">

yes

</td>
<td valign="top">

Enables Continuous Backup.

</td>
</tr>
<tr>
<td valign="top">

backupRetentionPeriod

</td>
<td valign="top">

integer

</td>
<td valign="top">

no

</td>
<td valign="top">

Number of days backup is retained, between 1 and 35. If not provided, Object Store Service sets a retention period of 14 days by default.

</td>
</tr>
</table>

The command above accomplishes the following:

-   Enables continuous backup on the source bucket.
-   Configures the expiration rule to automatically delete a backup older than *n* number of days.

> ### Note:  
> You can also use this command to update the retention period for an existing backup configuration.

**Related Information**  


[https://docs.aws.amazon.com/aws-backup/latest/devguide/s3-backups.html](https://docs.aws.amazon.com/aws-backup/latest/devguide/s3-backups.html)

