<!-- loiob03c5b90727545a09a5d175040e67c51 -->

# Server Access Logging

Object Store service allows users to enable server access logging feature on a S3 bucket. The feature helps in capturing detailed logs of various requests that are performed on the source bucket \(bucket created via service instance creation\).

Enabling server access logging through Object Store service leads to creation of a target bucket to store logs, along with enablement of read access to the logs. In addition, a default retention period is set after which the logs get deleted automatically.

Object Store service keeps server access logging disabled by default. It can be enabled during the create-service call or at any time later using the update-service call.

> ### Note:  
> This feature isn’t applicable for the service instances that are created before the feature was released.

For more details related to server access logging on AWS S3, please refer the Amazon's documentation: [Server Logs](https://docs.aws.amazon.com/AmazonS3/latest/dev/ServerLogs.html).



<a name="loiob03c5b90727545a09a5d175040e67c51__section_t55_cxg_dmb"/>

## List of Configuration Parameters


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

enableSAL

</td>
<td valign="top">

boolean

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Enables or disables server access logging

</td>
</tr>
<tr>
<td valign="top">

salLogsRetentionPeriod

</td>
<td valign="top">

Integer

</td>
<td valign="top">

No

</td>
<td valign="top">

Sets or removes object-expiration rule on target bucket.

\- Positive value: configures expiration rule on target bucket, to delete logs after n number of days from the date of creation of logs, where n is the input value provided

\- Zero or negative value: removes expiration rule if already present, to never delete logs.

\- No value is specified: configures expiration rule on target bucket to delete logs older than 365 days.

</td>
</tr>
</table>



<a name="loiob03c5b90727545a09a5d175040e67c51__section_yst_fxg_dmb"/>

## Enable Server Access Logging and Access Logs

Create a service instance with following command:

```
cf create-service <service_instance_name> -c '{"enableSAL":true,"salLogsRetentionPeriod":<n>}'
```

Update the service instance with following command:

```
cf update-service <service_instance_name> -c '{"enableSAL":true,"salLogsRetentionPeriod":<n>}'
```

The command does the following:

-   Ensure that a target bucket is present, if it doesn't exist already, else create a bucket.
-   Enable server access logging on the source bucket and configure the logs to get stored in the target bucket.
-   Configure object expiration rule to automatically delete logs that are older than \`n\` number of days from the target bucket.

Once the service instance is updated, status of server access logging along with the target bucket and target prefix can be obtained by following command: This

```
aws s3api get-bucket-logging --bucket <source_bucket_name>
```

command returns server access logging configuration on source bucket. Users have read-only access to target bucket and logs are put with prefix as mentioned.

```

{
    "LoggingEnabled": {
        "TargetPrefix": "logs/<source_bucket_name>/", 
        "TargetBucket": "<target_bucket_name>"
    }
}
```



<a name="loiob03c5b90727545a09a5d175040e67c51__section_ykp_qxg_dmb"/>

## Disable Server Access Logging

Update the service instance with following command to disable logging on source bucket:

```

cf update-service <service_instance_name> -c '{"enableSAL":false}'
```

The command disables server access logging on source bucket. However, the logs remain in the target bucket as per the retention period provided during enablement of this feature. Users continue to have read-only access to the target bucket in order to access logs captured so far.

> ### Note:  
> -   Whenever the \``cf create-service`\` or \``cf update-service`\` command is triggerd with \`enableSAL\` as \`true\`, if the \`salLogsRetentionPeriod\` isn’t provided, the default value is taken for this parameter \(365 days\).
> 
>     Whenever the \``cf create-service`\` or \``cf update-service`\` command is triggerd with \`enableSAL\` as \`true\`, if the \`salLogsRetentionPeriod\` is negative, OSaaS removes log expiration rule from target bucket.
> 
>     Whenever the \``cf create-service`\` or \``cf update-service`\` command is triggerd with \`enableSAL\` as \`false\`, value for \`salLogsRetentionPeriod\` isn't considered.
> 
> -   Whenever the \``cf delete-service`\` command is triggered, the target bucket having the logs are deleted immediately, along with the source bucket that has the data. This is irrespective of the logs retention period that was last set.



<a name="loiob03c5b90727545a09a5d175040e67c51__section_ksc_fyg_dmb"/>

## Impact on Cost

The logs stored in the target bucket are charged in the same way as the source bucket where data is stored.

Object Store service never deletes the logs explicitly on disablement of the server access logging feature. The logs continue to remain and are charged for, until they get deleted automatically, based on the last configured retention policy or the corresponding service instance itself is deleted.

