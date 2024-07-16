<!-- loiof95653ea3ffe4eaeaf665c84d2edf8c1 -->

# Java Code Snippets

You can use the following sample code snippets as a reference:



-   Read VCAP\_SERVICES

    > ### Sample Code:  
    > ```
    > @Value("${vcap.services.objectstore.credentials.account_name}")  
    > String accountName; 
    > 
    > @Value("${vcap.services.objectstore.credentials.container_name}")  
    > String containerName;  
    > 
    > @Value("${vcap.services.objectstore.credentials.container_uri}")  
    > String containerUri;  
    > 
    > @Value("${vcap.services.objectstore.credentials.sas_token}")  
    > String sasToken;  
    > 
    > @Value("${vcap.services.objectstore.credentials.region}")   
    > String region;  
    > ```

-   Get container reference

    > ### Sample Code:  
    > ```
    > CloudBlobContainer cloudBlobContainer = new CloudBlobContainer(new URI(containerUri + "?" + sasToken));
    > ```

-   Get BlockBlob reference

    > ### Sample Code:  
    > ```
    > String blobName = "test-blob-1";
    > CloudBlockBlob cloudBlockBlob = new CloudBlockBlob(new URI(containerUri + "/" + blobName + "?" + sasToken));
    > ```

-   List blobs in the container

    > ### Sample Code:  
    > ```
    > for (ListBlobItem listBlobItem : cloudBlobContainer.listBlobs()) {
    > 	System.out.println("Storage URI: " + listBlobItem.getStorageUri());
    > }
    > ```

-   Upload blob

    > ### Sample Code:  
    > ```
    > String blobContent = "This is blob content text.";
    > InputStream inputStream = new ByteArrayInputStream(blobContent.getBytes("UTF-8"));
    > cloudBlockBlob.upload(inputStream, blobContent.length());
    > ```

-   Download blob

    > ### Sample Code:  
    > ```
    > OutputStream outputStream = new ByteArrayOutputStream();
    > cloudBlockBlob.download(outputStream);
    > ```

-   Delete Blob

    > ### Sample Code:  
    > ```
    > cloudBlockBlob.deleteIfExists();
    > ```


Instead of providing blob content as text, you can provide blobs by providing file path. For more information, see [Blob operations](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-java-how-to-use-blob-storage#upload-a-blob-into-a-container).

