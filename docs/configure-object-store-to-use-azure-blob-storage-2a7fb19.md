<!-- loio2a7fb19e06334534a3b999da1b343559 -->

# Configure Object Store to use Azure Blob Storage

The Object Store service in the Azure landscape provides Azure BlobStorage containers as object store resource.



## Context

The Object Store service supports following operations: Create Azure BlobStorage container \(Service instance\), delete container, create credentials to access the container via cf bind-service and create-service-key call, and delete credentials via cf unbind-service and delete-service-key call.



## Procedure

Example on how to perform create-service & bind service operations:

The following example shows how you can create an instance of object store service with standard plan. Similarly, it can also be done for the other supported plans.

1.  Look for the service on Cloud Foundry using the command `cf marketplace`. You can see a service called "objectstore", with the plan "standard."

    ```
    Service: objectstore  
    Plans: standard  
    Description: Objectstore service  
    ```

2.  Create a service instance using the command `cf create-service objectstore standard <serviceInstanceName>`.

3.  List the services available using the command `cf services`. There's a time delay before the operation gets completed, until which in progress could be seen under last operation field.

    ```
    Name || Service || Plan || Bound apps |
    | Last operation <serviceInstanceName> || objectstore || standard || || create-succeeded 
    ```

4.  Create a service key to generate credentials to access the storage`cf create-service-key <serviceInstanceName> <keyName>` 

5.  Get service key credentials using which you could now access the storage `cf service-key <serviceInstanceName> <keyName>` .

    Sample output is:

    ```
    { 
    "credentials": 
    { 
    	"account_name": "<storage_account_name>", 
    	"container_name": "<container_name_corresponding_to_service_instance>", 
    	"container_uri": "<container_uri>", 
    	"sas_token": "<sas_token>", 
    	"region": "<azure_container_region>" 
    }
    ```

6.  To bind your application with the service key, execute the following steps:

    1.  Create a user provided service using the service key by providing the credentials JSON as input to the command : `cf create-user-provided-service`

    2.  Bind your application with the user provided service using the command : `cf bind-service <applicationName> <userProvidedServiceName>`


7.  You can skip the steps from 4 to 6 and directly bind objectstore service instance to your applications using the following command: `cf bind-service <applicationName> <serviceInstanceName>`.

8.  The credentials can then be read from the application environment under VCAP\_SERVICES:`cf env <applicationName>`.

    Output:

    ```
    { 
    "VCAP_SERVICES": { 
    "objectstore": [ 
    { 
    	"credentials": { 
    	"account_name": "<storage_account_name>", 
    	"container_name": "<container_name_corresponding_to_service_instance>", 
    	"container_uri": "<container_uri>", 
    	"sas_token": "<sas_token>", 
    	"region": "<azure_container_region>" 
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

    -   `account_name`: Name of the storage account
    -   `container_name`: Name of the container created within the storage account
    -   `container_uri`: Container URI
    -   `sas_token`: Service SAS token needed to access container
    -   `region`: The region in which the storage account and container are created

    > ### Note:  
    > If your use case requires having more than five applications bound to a single service instance, use the service key approach described in steps 4 to 6 to overcome the limitation of five service bindings and service keys.


