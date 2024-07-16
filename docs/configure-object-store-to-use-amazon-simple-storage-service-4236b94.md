<!-- loio4236b942f67349d5a583773162d99660 -->

# Configure Object Store to use Amazon Simple Storage Service

Object Store service on AWS based landscapes provides AWS S3 buckets as object store resources.



## Context

Object Store service provisions an AWS S3 bucket as part of the object store service instance creation. It generates credentials in the form of AWS IAM technical user during service binding or service key creation operations. The service also supports invalidating and deleting the credentials as part of service unbind and service key deletion operations. In addition, it supports service instance update and delete operations.



<a name="loio4236b942f67349d5a583773162d99660__steps_zyq_lpt_1y"/>

## Procedure

Example on how to perform create-service & bind service operations. Similarly, it can also be done for the other supported plans.

1.  Look for the service on Cloud Foundry using the command: `cf marketplace`. A service called “objectstore” with the plan “standard” is available.

    ```
    Service: objectstore Plans: standard Description: Objectstore service
    ```

2.  Create an instance of the service using the command `cf create-service objectstore standard` *<serviceInstanceName\>*.

3.  List the service instance using the command `cf services` and you can find create-succeeded after the service instance creation is completed. Please note that it might take a while before the operation gets completed, until which*in progress* could be seen under *last operation* field. The output lists the service instance details.

    ```
    Name || Service || Plan || Bound apps || Last operation 
    <serviceInstanceName> || objectstore || standard || || create-succeeded
    ```

4.  Create a service key to generate credentials to access the storage `cf create-service-key <serviceInstanceName> <keyName`\>

5.  Get service key credentials using which you could now access the storage`cf service-key <serviceInstanceName> <keyName>`.

    The output of the command is:

    ```
    "credentials": 
    { 
    	"access_key_id": "<some_access_key_id>", 
    	"bucket": "<some_bucket_name>", 
    	"host": "<region_specific_s3_endpoint>", 
    	"region": "<region>", 
    	"secret_access_key": "<some_secret_access_key>", 
    	"uri": "s3://<some_access_key_id>:<some_secret_access_key>@<region_specific_s3_endpoint>/<some_bucket_name>",
    	"username": "<some_username>" 
    }
    ```

6.  To bind your application with the service key, execute the following steps:

    1.  Create a user provided service using the service key by providing the above credentials JSON as input to the command : `cf create-user-provided-service`

    2.  Bind your application with the user provided service using the command : `cf bind-service <applicationName> <userProvidedServiceName>`


7.  You may skip the steps from 4 to 6 and directly bind object store service instance to your applications using the following command: `cf bind-service <applicationName> <serviceInstanceName>` 

8.  The credentials can then be read from the application environment under VCAP\_SERVICES: `cf env <applicationName>`

    ```
    { 
    "VCAP_SERVICES": { 
    "objectstore": [ 
    { 
    	"credentials": { 
    	"access_key_id": "<some_access_key_id>", 
    	"bucket": "<some_bucket_name>", 
    	"host": "<region_specific_s3_endpoint>", 
    	"region": "<region>", 
    	"secret_access_key": "<some_secret_access_key>", 
    	"uri": "s3://<some_access_key_id>:<some_secret_access_key>@<region_specific_s3_endpoint>/<some_bucket_name>", 
    	"username": "<some_username>" 
    	}, 
    	"label": "objectstore", 
    	"name": "<serviceInstanceName>", 
    	"plan": "standard", 
    	"provider": null, 
    	"syslog_drain_url": null, 
    	"tags": [ 
    	"blobStore", 
    	"objectStore" 
    	], 
    	"volume_mounts": [] 
       }
      ] 
     } 
    }
    ```

9.  Description of the parameters that are part of the credentials:

    -   `bucket`: Name of the AWS S3 bucket provisioned
    -   `access_key_id`: Access Key ID of the AWS IAM technical user created
    -   `secret_access_key`: Secret Key ID of the AWS IAM technical user created
    -   `host`: Host Name
    -   `region`: Region in which the AWS S3 bucket is provisioned
    -   `username`: AWS IAM user name
    -   `uri`: URI for the bucket

    > ### Note:  
    > In case your use-case requires having more than 5 applications bound to a single service instance at any given time, you may use the service key approach described above in steps 4 to 6 to overcome the limitation of 5 service bindings and service keys.


