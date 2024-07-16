<!-- loio4a7e6d7183f94048bfa74c3b4e1f2f76 -->

# Data Encryption Strategy

Object Store service supports default server side encryption on buckets and containers that are created through the service. Object Store service doesn't have control over how it is done internally by the underlying infrastructure.


<table>
<tr>
<th valign="top">

Data Center

</th>
<th valign="top">

Data stored on persistent disk

</th>
<th valign="top">

Reference

</th>
</tr>
<tr>
<td valign="top">

Amazon Web Service

</td>
<td valign="top">

Amazon S3 server-side encryption uses one of the strongest block ciphers available, 256-bit Advanced Encryption Standard \(AES-256\), to encrypt your data. Amazon ensures that each object is encrypted with a unique key. As an additional safeguard, it encrypts the key itself with a master key that it regularly rotates. This means that there is no additional configuration needed from customer for having default server side encryption. However, how it is internally done is completely abstracted from SAP.

</td>
<td valign="top">

[Bucket Encryption](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html)

</td>
</tr>
<tr>
<td valign="top">

Microsoft Azure

</td>
<td valign="top">

Azure Storage automatically encrypts your data when persisting it to the cloud using Microsoft-managed keys. Data in Azure Storage is encrypted and decrypted transparently using 256-bit AES encryption, one of the strongest block ciphers available. Again, SAP doesn’t have any control over how this is done by Azure.

</td>
<td valign="top">

[Data Encryption](https://docs.microsoft.com/en-us/azure/storage/common/storage-service-encryption#:~:text=the%20rotation%20yourself.-,Encryption%20scopes%20for%20Blob%20storage%20(preview),key%20that%20encrypts%20your%20data.)

</td>
</tr>
<tr>
<td valign="top">

GCP

</td>
<td valign="top">

Makes use of 256-bit AES algorithm for encrypting data by default. This is totally controlled by GCP and the internal working is abstracted from SAP.

</td>
<td valign="top">

[Default Keys](https://cloud.google.com/storage/docs/encryption/default-keys)

</td>
</tr>
</table>

