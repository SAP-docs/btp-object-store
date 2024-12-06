<!-- loio644df4fec0ca491482056e0a8db21e03 -->

# Capabilities of Object Store on Azure

Supported parameters of Object Store on Azure.




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
</table>

**Related Information**  


[Object Versioning](object-versioning-7c0f704.md "For instances created on the Zone Redundant Storage (ZRS) storage class, the Object Store service has a built-in capability that allows object (blob) versioning on Azure-based landscapes. Blob versioning is a feature provided by Azure.")

[Preventing Accidental Deletion of Azure Containers](preventing-accidental-deletion-of-azure-containers-67e5ba7.md "")

[Auto Expiration of Blobs and Blob Versions](auto-expiration-of-blobs-and-blob-versions-4162969.md "You can set certain rules to delete objects when you want to avoid manual clean-up of objects or reduce storage cost.")

