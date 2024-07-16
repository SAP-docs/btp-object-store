<!-- loio32517ae707c44ad48f635ea6bcbe271a -->

# Java Code Snippets



You can use the following sample code snippets as a reference:

-   Read VCAP\_SERVICES

    > ### Sample Code:  
    > ```
    > @Value("${vcap.services.objectstore.credentials.access_key_id}")  
    > String accessKeyId;  
    > @Value("${vcap.services.objectstore.credentials.secret_access_key}")  
    > String secretAccessKey;  
    > @Value("${vcap.services.objectstore.credentials.bucket}")  
    > String bucketName;
    > @Value("${vcap.services.objectstore.credentials.host}")   
    > String endPoint;
    > @Value("${vcap.services.objectstore.credentials.region}")   
    > String bucketRegion; 
    >   
    > 
    > ```

-   Get an Amazon S3 client

    > ### Sample Code:  
    > ```
    > //Using setEndPoint method
    > AWSCredentials credentials = new BasicAWSCredentials(accessKeyId, secretAccessKey);
    > AmazonS3 s3client = null;
    > s3client = new AmazonS3Client(credentials);
    > s3client.setEndPoint(endPoint);
    > 
    > //Using region method
    > AWSCredentials credentials = new BasicAWSCredentials(accessKeyId, secretAccessKey);
    > AmazonS3 s3client = null;
    > s3client = new AmazonS3Client(credentials);   
    > s3client.setRegion(bucketRegion);   
    > ```

-   Upload an object

    > ### Sample Code:  
    > ```
    > s3client.putObject(new PutObjectRequest(bucketName, objectName, file));
    > ```

-   Download an object

    > ### Sample Code:  
    > ```
    > s3client.getObject(new GetObjectRequest(bucketName, objectName));
    > 
    > ```

-   Delete an object

    > ### Sample Code:  
    > ```
    > s3client.deleteObject(bucketName, objectName);
    > ```


