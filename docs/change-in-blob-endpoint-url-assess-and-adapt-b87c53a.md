<!-- loiob87c53a89ba447b7804d1001a44e3971 -->

# Change in Blob Endpoint URL: Assess and Adapt

BTP Object Store Service on Azure has been internally enhanced to achieve improved IaaS resources scalability.

This will cause a change in `blob endpoint URL` in `container_uri`, that is one of the parameters of `objectstore` service credentials.

The endpoint of storage accounts will change to this format:`storageAccountName.[dnszone].blob.storage.azure.net`, where dnszone can be between `z00` and `z99`.



<a name="loiob87c53a89ba447b7804d1001a44e3971__section_wy1_hws_4wb"/>

## Are you impacted?

Consumers who are already fetching blob endpoint from`container_uri` \(that is one of the parameters of `objectstore` service credential\) and passing the same as an argument while performing various operations, require no code change.

But, consumers need to adapt if:

-   Blob endpoint URL is constructed by appending`.blob.core.windows.net` at the end of the `account_name` \(obtained via `objectstore` service credentials\), or

-   In Azure CLI commands,`--account-name` is passed instead of `--blob-endpoint`, alongside `--container-name` & `--sas-token`.



<a name="loiob87c53a89ba447b7804d1001a44e3971__section_qvw_b1t_4wb"/>

## How you need to adapt?

If you are impacted based on the above description, you need to upgrade your SDK/tools as listed below and adapt accordingly:


<table>
<tr>
<th valign="top">

SDK/Tools

</th>
<th valign="top">

Version

</th>
</tr>
<tr>
<td valign="top">

Storage Management API

</td>
<td valign="top">

2021-09-01 or later

</td>
</tr>
<tr>
<td valign="top">

Azure SDK for .Net

</td>
<td valign="top">

Azure.Storage.Common 12.8.0 or later

Azure.Storage.Files.DataLake 12.7.0 or later

[https://www.nuget.org/packages/Azure.Storage.Blobs/](https://www.nuget.org/packages/Azure.Storage.Blobs/)

</td>
</tr>
<tr>
<td valign="top">

Azure SDK for JAVA

</td>
<td valign="top">

azure-storage-blob v12.10.0 or later

azure-storage-common v12.10.0 or later

azure-storage-file-datalake v12.4.0 or later

[https://mvnrepository.com/artifact/com.azure/azure-storage-blob](https://mvnrepository.com/artifact/com.azure/azure-storage-blob)

</td>
</tr>
<tr>
<td valign="top">

Azure SDK for JS

</td>
<td valign="top">

No support yet

Estimated date to add support is middle of June 2022

</td>
</tr>
<tr>
<td valign="top">

Azure SDK for Python

</td>
<td valign="top">

azure-storage-blob v12.7.0 \(including 12.7.0b1\)

azure-storage-file-datalake v12.2.0

[https://pypi.org/project/azure-storage-blob/](https://pypi.org/project/azure-storage-blob/)

</td>
</tr>
<tr>
<td valign="top">

Azure Powershell

</td>
<td valign="top">

Az.Storage 4.4.2 and later

[https://github.com/Azure/azure-powershell/](https://github.com/Azure/azure-powershell/)

</td>
</tr>
<tr>
<td valign="top">

Azure CLI

</td>
<td valign="top">

Azure CLI 2.37.0 or above

[https://github.com/Azure/azure-cli](https://github.com/Azure/azure-cli)

</td>
</tr>
<tr>
<td valign="top">

AzCopy

</td>
<td valign="top">

v10.9.0 or later

[https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)

</td>
</tr>
<tr>
<td valign="top">

Azure Storage Explorer

</td>
<td valign="top">

1.19.0 or later

[https://azure.microsoft.com/en-us/features/storage-explorer/](https://azure.microsoft.com/en-us/features/storage-explorer/)

</td>
</tr>
<tr>
<td valign="top">

Management plane SDK

</td>
<td valign="top">

24.0.0 or later

</td>
</tr>
</table>



<a name="loiob87c53a89ba447b7804d1001a44e3971__section_vjx_wbt_4wb"/>

## Code snippets and examples for reference

*Sample blob endpoint URL*

The only change in the service credential is the format of the endpoint in `container_uri`as shown below:

> ### Sample Code:  
> ```
> {
> 	"credentials": {
> 		"account_name": "<storage account name>",
> 		"container_name": "<container_name>",
> 		"container_uri": "https://<storage_account_name>.z17.blob.storage.azure.net/<container_name>",
> 		"region": "westeurope",
> 		"sas_token": "<SAS_token>"
> 	}
> }
> ```

Therefore, the blob endpoint has to be extracted from `container_uri` field and its value for the above sample service credential is `https://storage_account_name>.z17.blob.storage.azure.net/`.



<a name="loiob87c53a89ba447b7804d1001a44e3971__section_cr2_c2t_4wb"/>

## Guidance on adapting in scripts that use Azure CLI

While using Azure CLI, `blob-endpoint` should be passed as shown below:

-   To upload a blob

    `az storage blob upload --file $localFile --name $blobName --container-name $containerName --blob-endpoint $blobEndpoint`

-   To download a blob

    `az storage blob download --file $localFile --name $blobName --container-name $containerName --blob-endpoint $blobEndpoint`




<a name="loiob87c53a89ba447b7804d1001a44e3971__section_ncl_ssy_4wb"/>

## Guidance on adapting applications/scripts using various SDKs/tools:

The blob endpoint should be extracted as described above and passed correctly while performing object upload/download operations.

-   Sample code snippet for Python:

    > ### Sample Code:  
    > ```
    > from azure.storage.blob import BlobClient  
    > 
    > sas_url = "https://test-account.z17.blob.storage.azure.net/test-container-zrs/myBlob?sv=2021-08-06&spr=https&si=9311c0aa-35f3-4166-a2d0-6696063c7146&sr=c&sig=Z7OQ3guYpC7mE7YPULBGKYGCrjPDdn7IixN9IG%2BCh0Y%3D"     
    > 
    > blob_client = BlobClient.from_blob_url(sas_url)     
    > 
    > with open("./SampleSource.txt", "rb") as data:     
    >        blob_client.upload_blob(data) 
    > ```

-   Sample code snippet for Java:

    > ### Sample Code:  
    > ```
    > try {     
    >     File file = new File("src/main/resources/Sample.txt");     
    >     InputStream targetStream = new FileInputStream(file);     
    >     
    >     BlobContainerClient blobContainerClient = new BlobContainerClientBuilder()     
    > 	    .endpoint("https://test-account.z17.blob.storage.azure.net/")     
    > 	    .containerName("test-container")     
    > 	    .sasToken("si=testpolicy&spr=https&sv=2021-06-08&sr=c&sig=5HUKJD2d%2FexcTTrU2vnry0VU6Mz74eAMSWMA2C8lmY0%3D")     
    > 	    .buildClient();     
    > 	    
    >     BlobClient blobClient = blobContainerClient.getBlobClient("test");     
    >     blobClient.upload(targetStream, file.length());     
    >     
    > } catch (Exception ex) {     
    >     ex.printStackTrace();     
    > }  
    > ```


