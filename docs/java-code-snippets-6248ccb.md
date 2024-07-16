<!-- loio6248ccbf3e12417eab39aa207f80ed66 -->

# Java Code Snippets



You can use the following sample code snippets as a reference:

-   Read VCAP\_SERVICES

    > ### Sample Code:  
    > ```
    > @Value("${vcap.services.objectstore.credentials.base64EncodedPrivateKeyData}")  
    > String base64EncodedPrivateKeyData;  
    > 
    > @Value("${vcap.services.objectstore.credentials.projectId}")  
    > String projectId;   
    > 
    > @Value("${vcap.services.objectstore.credentials.keyAlgo}")   
    > String keyAlgo;   
    > 
    > @Value("${vcap.services.objectstore.credentials.region}")   
    > String bucketRegion;   
    > 
    > @Value("${vcap.services.objectstore.credentials.bucket}")  
    > String bucketName;  
    >   
    > 
    > ```

-   Get Storage Client

    > ### Sample Code:  
    > ```
    > String credentials = Base64.decodeBase64(base64EncodedPrivateKeyData).toString();
    > InputStream is = new ByteArrayInputStream(credentials.getBytes(Charset.forName("UTF-8")));
    > ServiceAccountCredentials sac = ServiceAccountCredentials.fromStream(is);
    > Storage storageClient = StorageOptions.newBuilder()
    > 		.setProjectId(projectId)
    > 		.setCredentials(sac)
    > 		.build()
    > 		.getService();  
    > ```

-   Upload an object

    > ### Sample Code:  
    > ```
    > BlobId blobId = BlobId.of(bucketName, <path_to_object>);
    > // Here, <path_to_object> = <path1>/<path2>/objectName;
    > 
    > BlobInfo blobInfo = null;
    > blobInfo = BlobInfo.newBuilder(blobId)
    > 	.setContentType("text/plain")
    > 	.build();
    > String content = <content to upload>;
    > storageClient.create(blobInfo, content.getBytes(Charset.forName("UTF-8")));
    > ```

-   Download an object

    > ### Sample Code:  
    > ```
    > Blob blob = null;
    > BlobId blobId = BlobId.of(bucketName, <path_to_object>);
    > // Here, <path_to_object> = <path1>/<path2>/objectName;
    > 
    > String blobContent = null;
    > blob = storageClient.get(blobId);
    > blobContent = new String(blob.getContent(), Charset.forName("UTF-8"));
    > ```

-   Delete an object

    > ### Sample Code:  
    > ```
    > BlobId blobId = BlobId.of(bucketName, <path_to_object>);
    > // Here, <path_to_object> = <path1>/<path2>/objectName;
    > storageClient.delete(blobId);
    > ```


