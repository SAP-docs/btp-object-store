<!-- loio8ec6f596ce5d4c1aa0c23d07a21bfe24 -->

# Capabilities of Object Store on AWS

Supported parameters of Object Store on AWS.




<table>
<tr>
<th valign="top">

Parameter

</th>
<th valign="top">

Supported in create call

</th>
<th valign="top">

Supported in update call

</th>
<th valign="top">

Supported in create call, together with other parameters

</th>
<th valign="top">

Supported in update call, together with other parameters

</th>
</tr>
<tr>
<td valign="top">

versioning

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Yes

</td>
</tr>
<tr>
<td valign="top">

preventDeletion

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Yes

</td>
</tr>
<tr>
<td valign="top">

autoExpiration

</td>
<td valign="top">

No

</td>
<td valign="top">

Yes

</td>
<td valign="top">

No

</td>
<td valign="top">

Yes

</td>
</tr>
<tr>
<td valign="top">

deleteAutoExpiration

</td>
<td valign="top">

No

</td>
<td valign="top">

Yes

</td>
<td valign="top">

No

</td>
<td valign="top">

No

</td>
</tr>
<tr>
<td valign="top">

enableSAL && salLogsRetentionPeriod

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Yes

</td>
</tr>
<tr>
<td valign="top">

backupEnabled && backupRetentionPeriod

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Yes

</td>
<td valign="top">

Yes

</td>
</tr>
</table>

**Related Information**  


[Object Versioning](object-versioning-787fbe7.md "Object versioning helps in keeping multiple versions of the same object. Versioning automatically maintains previous versions of an object.")

[Object Expiration Rules](object-expiration-rules-52e2c18.md "Object Expiration allows you to schedule removal of your objects after a defined time period. It helps define rules to expire objects within a bucket based on which Amazon S3 deletes expired objects.")

[Server Access Logging](server-access-logging-b03c5b9.md "Object Store service allows users to enable server access logging feature on a S3 bucket. The feature helps in capturing detailed logs of various requests that are performed on the source bucket (bucket created via service instance creation).")

[Prevent Accidental Deletion of AWS S3 Buckets](prevent-accidental-deletion-of-aws-s3-buckets-8c3c66d.md "On initiating service instance deletion call, Object Store service ensures deletion of service instance resources, which includes AWS S3 bucket(s), and hence the objects in the bucket also gets deleted.")

[Retrieve Parameters Configured on Service Instance](retrieve-parameters-configured-on-service-instance-def55f9.md "")

[Role-Based Bindings and Service Keys \(AWS\)](role-based-bindings-and-service-keys-aws-d33b31a.md "Object Store supports creating service credentials with read and write roles. This allows applications to be bound to role-specific service bindings to restrict access per use case.")

