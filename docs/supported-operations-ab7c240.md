<!-- loioab7c2406d8b349f584342663f83e485a -->

# Supported Operations

The Object Store service provides a role named storage object admin to each binding or a service key user.



The role grants full control over objects including listing, creating, viewing, and deleting objects. The list of operations supported would include the following:


<table>
<tr>
<td valign="top">

storage.objects.create

</td>
<td valign="top">

Add new objects to a bucket.

</td>
</tr>
<tr>
<td valign="top">

storage.objects.delete

</td>
<td valign="top">

Delete objects.

</td>
</tr>
<tr>
<td valign="top">

storage.objects.get

</td>
<td valign="top">

Read object data and metadata, excluding ACLs.

</td>
</tr>
<tr>
<td valign="top">

storage.objects.getIamPolicy

</td>
<td valign="top">

Read object ACLs, returned as IAM policies.

</td>
</tr>
<tr>
<td valign="top">

storage.objects.list

</td>
<td valign="top">

List objects in a bucket. Also, read object metadata, excluding ACLs, when listing.

</td>
</tr>
<tr>
<td valign="top">

storage.objects.setIamPolicy

</td>
<td valign="top">

Update object ACLs.

</td>
</tr>
<tr>
<td valign="top">

storage.objects.update

</td>
<td valign="top">

Update object metadata, excluding ACLs.

</td>
</tr>
<tr>
<td valign="top">

storage.multipartUploads.create

</td>
<td valign="top">

Upload objects in multiple parts.

</td>
</tr>
<tr>
<td valign="top">

storage.multipartUploads.abort

</td>
<td valign="top">

Abort multipart upload sessions.

</td>
</tr>
<tr>
<td valign="top">

storage.multipartUploads.listParts

</td>
<td valign="top">

List the uploaded object parts in a multipart upload session.

</td>
</tr>
<tr>
<td valign="top">

storage.multipartUploads.list

</td>
<td valign="top">

List the multipart upload sessions in a bucket.

</td>
</tr>
</table>

> ### Note:  
> -   The Object Store service keeps access to all objects restricted to the service account user that it creates as part of service bindings and service keys. None of the objects residing in a GCS bucket are publicly accessible by default.
> 
> -   Access level of objects can change only if you set object ACLs.
> 
> -   We strongly recommend you to be careful when setting object ACLs for your buckets.

**Related Information**  


[Object permissions](https://cloud.google.com/storage/docs/access-control/iam-permissions)

[Buckets](https://cloud.google.com/storage/docs/json_api/v1/buckets)

[Objects](https://cloud.google.com/storage/docs/json_api/v1/objects)

