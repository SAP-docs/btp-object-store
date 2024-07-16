<!-- loio578bb0badf2f4da2a7b72dd2762e44aa -->

# Security of the ObjectStore-aaS Access Keys

A service broker in Cloud Foundry generates credentials during service binding and service key creation operations. It can invalidate the credentials only when the corresponding service unbinding or service key deletion operations are executed by the service consumer.

In case of ObjectStore-aaS, each customer gets access keys corresponding to a technical user in the IaaS account, when a \`\``cf bind-service`\`\` or \`\``cf create-service-key`\`\` operation is executed. These access keys are used by the ObjectStore-aaS consumer application. The technical user along with the access key is only deleted by the service broker, when the corresponding \`\``cf unbind-service`\`\` or \`\``cf delete-service-key`\`\` operation is triggered.

> ### Note:  
> For higher security, we strongly recommend the consumers of the service to periodically \(less than or equal to 90 days\) rotate the access keys by recreating bindings or service-keys, irrespective of whether those are currently being used or not.

One of the approaches to achieve the same is by making use of the standard blue-green deployment model for deploying applications.

> ### Note:  
> Security actions applied by AWS and GCP cloud provides to any publicly exposed Service Account Keys.
> 
> 1.  **GCP**: To enhance the security of customer environments, an organizational policy change from GCP will take effect starting June 2024. This change will proactively disable any publicly exposed Service Account Keys \(that you receive as part of service binding credentials from BTP Object Store Service\) that GCP becomes aware of. This will affect all uses of the exposed Service Account Key.
> 2.  **AWS**: As soon it is found that an access and secret key pair \(that you receive as part of service binding credentials from BTP Object Store Service\) have been public exposed, it stops allowing all object deletion and object version deletion operations through the exposed keys on the corresponding bucket and a security incident is raised to SAP and keys are also deactivated from SAP side.
> 
> In such cases, we advise you to rotate the corresponding service binding / service key as soon as possible, to get the key rotated and to get back all relevant permissions.
> 
> As users of the Object Store Service, if you face access-related issues with any existing binding credential being impacted due to above security measures, you are advised to delete the existing binding and create a new binding.

