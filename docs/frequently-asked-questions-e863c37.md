<!-- loioe863c371a7c84ae28dcf4afdc62456fb -->

# Frequently Asked Questions

Find answers to your common queries about Object Store on SAP BTP in the Cloud Foundry environment.



<a name="loioe863c371a7c84ae28dcf4afdc62456fb__section_vnq_yzm_42b"/>

## Why do we need object store against file store/block storage?


<table>
<tr>
<th valign="top">

 

</th>
<th valign="top">

Object Store

</th>
<th valign="top">

Block Store

</th>
</tr>
<tr>
<td valign="top">

Performance

</td>
<td valign="top">

Ideal for large content and high stream throughput

</td>
<td valign="top">

Strong performance with database and transactional data

</td>
</tr>
<tr>
<td valign="top">

Geography

</td>
<td valign="top">

Currently, ObjectStore-aaS provisions bucket/container in the same region as its underlying infrastructure.

For example, on Europe \(Frankfurt\) landscape, the buckets cannot be created in any other region apart from Europe \(Frankfurt\).

</td>
<td valign="top">

The further the distance between storage and application, the higher the latency

</td>
</tr>
<tr>
<td valign="top">

Scalability

</td>
<td valign="top">

Can scale infinitely to petabytes and beyond.

</td>
<td valign="top">

Addressing requirements limit scalability

</td>
</tr>
<tr>
<td valign="top">

Analytics

</td>
<td valign="top">

Customizable metadata allows data to be easily organized and retrieved.

</td>
<td valign="top">

No metadata

</td>
</tr>
</table>



<a name="loioe863c371a7c84ae28dcf4afdc62456fb__section_xmt_zzm_42b"/>

## Can Object Store be my primary database?

Object storage can be used either as primary storage or as external storage. When it’s used as primary storage, the object store only store the file content by using a unique identifier. No metadata are stored in the object store: no files names, no directory structures, etc.



<a name="loioe863c371a7c84ae28dcf4afdc62456fb__section_klg_q14_m2b"/>

## What are the regions in which Object Store is available?

Get an overview on the availability of Object Store service according to region, infrastructure provider, and release status in SAP Discovery Center: [Service Catalog](https://discovery-center.cloud.sap/viewServices)

.



<a name="loioe863c371a7c84ae28dcf4afdc62456fb__section_l4s_rd5_h2b"/>

## Is my data encrypted?

Your crucial information stored in the database is maintained in a highly secure manner as we at SAP use the encryption capabilities provided by the underlying IaaS providers AWS, Azure, and GCP. Encryption details for each of the IaaS provide are described in [Data Protection and Privacy](data-protection-and-privacy-dab81b6.md).



<a name="loioe863c371a7c84ae28dcf4afdc62456fb__section_ftl_ych_qfb"/>

## How to use Postman to make object related calls on AWS?

To perform REST calls \(GET, PUT DELETE\) on the AWS S3 bucket using Postman, the following information needs to be provided:

-   **HTTP Method**: GET/PUT/DELETE
-   **URL**: https://<host\>/<bucketName\>/<objectName\>
-   **AWS AccessKey**: access\_key\_id - The key that get from the credentials json \(on binding or creating service key\).
-   **AWS SecretKey**: secret\_access\_key - The key that you get from the credentials json \(on binding or creating service key\).
-   **AWS Region**: region - The region name that get from the credentials json \(on binding or creating service key\).
-   **Service Name**: s3 - This key isn’t passed in the credentials json, since Objectstore uses only S3, value to be used will be a constant: "s3"

    For GET Objects in a bucket \(List objects API\), you can use the following URL: https://<host\>/bucketName\>




<a name="loioe863c371a7c84ae28dcf4afdc62456fb__section_u3h_m2h_qfb"/>

## Is there a way to view uploaded images on the SAP BTP Cockpit?

We don’t have a UI console for the Object Store service instance today, so sorry SAP BTP cockpit won’t help you to view the uploaded images. However, you can make a List Objects API \(GET call mentioned above\) from Postman or from code to view the uploaded objects.



<a name="loioe863c371a7c84ae28dcf4afdc62456fb__section_d1v_n2h_qfb"/>

## How do I create or upload a blob on Azure?

1. Use the Request Method : PUT

2. Blob end point : <container\_uri\>/<objectname\>?<sass-token\> <container\_uri\> as obtained from the credentials after binding to object store service instance.

3. Headers : x-ms-blob-type:BlockBlob

Note : The http header "x-ms-blob-type" with value "BlockBlob" is mandatory to upload a blob using this request.



<a name="loioe863c371a7c84ae28dcf4afdc62456fb__section_udj_4tp_hkb"/>

## I've reached the maximum size for put Blob. What can I do?

MS Azure on PUT block blob operation, supports, only 256 MB max size file on a single HTTP request \(PUT API\). To support blob sizes of more than 256 MB, Azure suggests to upload the blobs in chunks of 256 MB and then call PUT Block List to combine all chunks as single blob \(kind of multipart upload scenario\). See the following documentation by Azure for more details:

-   [Size limitation on PUT API](https://docs.microsoft.com/en-us/rest/api/storageservices/put-blob#remarks)
-   [PUT Block list API](https://docs.microsoft.com/en-us/rest/api/storageservices/put-block-list)
-   [Sample code to solve this size limitation problem \(in C\#\)](https://inside.covve.com/uploading-block-blobs-larger-than-256-mb-in-azure/)



<a name="loioe863c371a7c84ae28dcf4afdc62456fb__section_at1_r2h_qfb"/>

## How do I enable a service plan for a particular region

Suppose you wanr to enable a plan in the Europe \(Frankfurt\) region. The subaccount has to be in the same region.

In the required region, perform the following steps:

1.  Choose *Global Account*
2.  Choose the subaccount tile with name : Sub Account name
3.  Choose *Spaces* on the left menu bar
4.  Create a space if it doesn't exist already
5.  Choose *Service Marketplace* under *Services* on the left menu bar.
6.  You should be able to see a tile named *ObjectStore*.

If the above mentioned steps don't help, then the service plan isn't enabled in a particular subaccount.

This can be verified by doing the following:

1.  Choose *Global Account*.
2.  Choose the *Entitlements* tab on the left menu bar.
3.  Look for *Object Store*.
4.  Verify if following entry is there - \["Your subaccount name", Europe \(Frankfurt\), s3-standard\].

If the entry isn't there, you may have to edit the page to add the plan in the subaccount.

This would allow you to see the service in the subaccount.



<a name="loioe863c371a7c84ae28dcf4afdc62456fb__section_thb_v34_smb"/>

## Following Error is Seen: "Error validating parameters: maximum size for put Blob is 256 MB", while uploading objects in Azure."

MS Azure on PUT block blob operation, supports, only 256 MB max size file on a single HTTP request \(PUT API\). To support blob sizes of more than 256 MB, Azure suggests uploadingto upload the blobs in chunks of 256 MB and then call PUT Block List to combine all chunks as single blob \(kind of multipart scenario\).

-   [Documentation by Azure on the size limitation on PUT API](https://docs.microsoft.com/en-us/rest/api/storageservices/put-blob#remarks)

-   [Documentation for For PUT Block list API](https://docs.microsoft.com/en-us/rest/api/storageservices/put-block-list).
-   [Sample code solve this size limitation problem \(in C\#\).](https://inside.covve.com/uploading-block-blobs-larger-than-256-mb-in-azure/)



<a name="loioe863c371a7c84ae28dcf4afdc62456fb__section_rtw_q55_h2b"/>

## I'm facing some technical problem. How do I seek support?

For any technical issues, please create a [support ticket](https://support.sap.com/en/index.html) with the component **BC-CP-CF-OSAAS**.

> ### Note:  
> Please find the[SAP Note](https://me.sap.com/notes/0001296527) for more information on how to create a support ticket.

