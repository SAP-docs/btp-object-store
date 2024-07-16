<!-- loio8751e18aa61240119a14ecea10b9d344 -->

# Supported and Unsupported Operations



## Supported Operations



### Operation supported on Buckets

-   ListBuckets
-   ListBucketMultipartUploads
-   GetBucketLocation
-   ListBucketVersions
-   GetBucketLogging \(Only when "Server Access Logging" is enabled. See [Server Access Logging](server-access-logging-b03c5b9.md) for more details\).



### Operations supported on Objects

-   Abort Multipart Upload
-   Delete Object
-   Delete Object Tagging
-   DeleteObjectVersion
-   DeleteObjectVersionTagging
-   Get Object
-   Get Object ACL
-   Get Object Torrent
-   Get Object Tagging
-   GetObjectVersion
-   GetObjectVersionAcl
-   List Multipart Upload Parts
-   Put Object ACL
-   Put Object Version ACL
-   Get a specific version of an object
-   Get object ACL \(for a specific version of an object\)
-   Put object tagging \(for a specific version of an object\)



<a name="loio8751e18aa61240119a14ecea10b9d344__section_qgv_1zy_sjb"/>

## Unsupported Operations

-   Enabling encryption with custom keys
-   AWS console access to buckets
-   Storage classes other than S3 standard.
-   Cross region replication
-   Access to Cloud watch metrics
-   Restoring a deleted bucket
-   Restoring an object transitioned to any other storage class from "standard" storage class

> ### Note:  
> To perform object related operations \(upload, download, delete etc\) users can directly make calls to AWS using the AWS SDKs.

For more information, see the [documentation](http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectOps.html) on the Amazon Web Services Web site.

