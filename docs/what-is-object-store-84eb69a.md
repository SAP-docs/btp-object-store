<!-- loio84eb69a421294ba0a407579490413dfa -->

# What Is Object Store?

Store and manage the blobs/objects on SAP BTP. 

Object Store service on SAP BTP lets you store and manage objects, which involves creation, upload, download, and deletion. This service is specific to the IaaS layer such as Azure Blob Storage, Amazon Web Services, and Google Cloud Platform.



As an application developer working on the SAP Business Technology Platform, you can use this service for storing objects. You can get access to storage space simply by provisioning an instance of the service, and the service handles any underlying technical complexities. Additionally, suppose your use case requires you to create several hundreds of storage resources. In that case, the service simplifies things for you to a great extent by internally taking care of accounts, resource management, and security-related configurations.



## Environment

This service supports consumption from multiple environments. See the Service Plans and Entitlements section for each IaaS to get details on the available plans in each environment.



## Features


<dl>
<dt><b>

Easy and secure access

</b></dt>
<dd>

Creates object store \(AWS S3 buckets, Azure Blob container or Google Cloud Storage buckets\) and passes secure credentials to the application to access the buckets.



</dd><dt><b>

High availability

</b></dt>
<dd>

Ensures that the storage for solutions is available to the maximum, without any interruptions.



</dd><dt><b>

High durability

</b></dt>
<dd>

Ensures durability as the underlying technologies that we use provide storage replication.



</dd><dt><b>

Scalability

</b></dt>
<dd>

Offers highly scalable storage that can be used by Cloud Foundry and Kyma applications to store and manage objects.



</dd>
</dl>



## Prerequisites

-   You must have SAP BTP Application Runtime.
-   You have a subaccount.
-   You have assigned entitlements and quotas to your subaccount in the SAP BTP global account. For more information, see [Configure Entitlements and Quotas for Subaccounts](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/5ba357b4fa1e4de4b9fcc4ae771609da.html?q=entitlements).

**Related Information**  


[Configure Object Store to use Azure Blob Storage](configure-object-store-to-use-azure-blob-storage-2a7fb19.md "The Object Store service in the Azure landscape provides Azure BlobStorage containers as object store resource.")

[Configure Object Store to use Amazon Simple Storage Service](configure-object-store-to-use-amazon-simple-storage-service-4236b94.md "Object Store service on AWS based landscapes provides AWS S3 buckets as object store resources.")

[Configure Object Store to use GCP](configure-object-store-to-use-gcp-687cd27.md "Object store service on GCP provides GCS bucket as object store resource.")

