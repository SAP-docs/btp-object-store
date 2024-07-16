<!-- loio687cd27b9383425fb0f64e9b0ea53a2c -->

# Configure Object Store to use GCP

Object store service on GCP provides GCS bucket as object store resource.



<a name="loio687cd27b9383425fb0f64e9b0ea53a2c__context_amz_1ww_rdb"/>

## Context

Object Store service provisions an GCS bucket as part of objectstore service instance creation. It generates credentials in the form of GCP IAM service account technical user during service binding or service key creation operations. The service also supports invalidating & deleting the credentials as part of service unbind & service key deletion operations. In addition, it supports service instance update and delete operations.



<a name="loio687cd27b9383425fb0f64e9b0ea53a2c__steps_bmz_1ww_rdb"/>

## Procedure

Example on how to perform create-service & bind service operations with `standard` plan. Similarly, it can also be done for the other supported plans.

1.  Look for available services on Cloud Foundry using the command `cf marketplace`. You can see a service called "objectstore" available with plan "standard.".

    ```
    Service: objectstore Plans: standard Description: Objectstore service
    ```

2.  Create a service instance of the above service and plan using the command`cf create-service objectstore standard <serviceInstanceName>`.

3.  List the services available using the command `cf services` and you can find create-succeeded after the service instance creation is completed. Please note that it might take a while before the operation gets completed, until which *in progress* could be seen under *last operation* field.

    ```
    Name || Service || Plan || Bound apps || Last operation
    <serviceInstanceName> || objectstore || standard
    ```

4.  Create a service key to generate credentials to access the storage `cf create-service-key <serviceInstanceName> <keyName>`

5.  Get service key credentials using which you could now access the storage. `cf service-key <serviceInstanceName> <keyName>`.

    A sample output:

    ```
    "credentials": 
    {
    	"base64EncodedPrivateKeyData": "<base64_encoded_service_account_credentials>", 
    	"projectId": "<project_id>", 
    	"keyAlgo": "<service_account_key_generation_algo>",
    	"region": "<region_of_bucket>", 
    	"bucket": "<some_bucket_name>" 
    }
    ```

6.  To bind your application to the service key, execute the steps below:

    1.  Create a user provided service using the service key by providing the above credentials JSON as input to the command : `cf create-user-provided-service`

    2.  Bind your application with the user provided service using the command: `cf bind-service <applicationName> <userProvidedServiceName>`


7.  You can also skip the above steps from 4 to 6 and directly bind the object store service instance to your applications using the following command: `cf bind-service <applicationName> <serviceInstanceName>`.

8.  The credentials can be read from application environment under VCAP\_SERVICES: `cf env <applicationName>`

    ```
    
    { 
    	"VCAP_SERVICES": { 
    	"objectstore": [ 
    { 
    	"credentials": { 
    	"base64EncodedPrivateKeyData": "<base64_encoded_service_account_credentials>", 
    	"projectId": "<project_id>", 
    	"keyAlgo": "<service_account_key_generation_algo>", 
    	"region": "<region_of_bucket>", 
    	"bucket": "<some_bucket_name>" 
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

    -   `base64EncodedPrivateKeyData`: Base 64 encoded string of the JSON credential of the service account
    -   `projectId`: GCP Project ID in which GCS bucket is created
    -   `keyAlgo`: Key Algorithm
    -   `region`: Region in which the bucket is created
    -   `bucket`: Name of the bucket provisioned as part of instance creation

    > ### Note:  
    > In case your use-case requires having more than 5 applications bound to a single service instance at any given time, you may use the service key approach described above in steps 4 to 6 to overcome the limitation of 5 service bindings and service keys.


