<!-- loio29bd26201a0c4d5c8cd922d3c0482677 -->

# Migrating Service Instances Created with LRS to ZRS

Steps for migrating existing service instances created with LRS to new instances with ZRS.



<a name="loio29bd26201a0c4d5c8cd922d3c0482677__prereq_f4s_s2z_tqb"/>

## Prerequisites

Ensure that the `AzCopy` utility is installed on the machine where the migration will be performed. You can download it from [Download AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10#download-azcopy).



## Context

This migration is applicable for object store instances created with azure-standard plan on Cloud Foundry only.



## Procedure

1.  Login to Cloud Foundry and the target to org / space where the existing service instance is present. Ensure that object store service access is still enabled in that org / space.

2.  For the migration purpose, an SAS token is required. Either existing binding/service-key credentials of existing instance can be used, or you may create a new service-key for migration purpose, as long as the total count of bindings does not surpass the limit of 5.

3.  Create a new service instance of object store with `azure-standard` plan. Create a service key for the same.

    The LRS based containers and ZRS based containers can be differentiated by the `zrs` suffix. LRS based containers would have `sapcp-osaas-<service_instance_guid>` and ZRS based containers would have `sapcp-osaas-<service_instance_guid>-zrs`.

4.  Execute following command using the respective SAS tokens obtained in service key credentials to initiate the migration activity. Please ensure that you remove `\u0026` from SAS tokens and replace it with `&`: `azcopy sync <source_container_uri_with_sas_token> <destination_container_uri_with_sas_token> --recursive=true`

    > ### Example:  
    > ```
    > $ azcopy sync "https://<source_account_name>.blob.core.windows.net/<source_container_name>?sig=somesig&sv=2019-02-02&spr=https&si=633edea9-3e66-48ea-8f8c-d75bf3f0d75e&sr=c" "https://<destination_account_name>.blob.core.windows.net/<destination_container_name>?sig=someothersig&sv=2019-02-02&spr=https&si=56d09ea5-0712-4d90-94fe-c5017c6f0b03&sr=c" --recursive=true
    > 
    > INFO: Any empty folders will not be processed, because source and/or destination doesn't have full folder support
    > 
    > Job a4b5eac1-b3e0-b94a-6c5a-2ed724fcbed6 has started
    > Log file is located at: /Users/<user>/.azcopy/a4b5eac1-b3e0-b94a-6c5a-2ed724fcbed6.log
    > 
    > 988 Files Scanned at Source, 101761 Files Scanned at Destination
    > 
    > Job a4b5eac1-b3e0-b94a-6c5a-2ed724fcbed6 Summary
    > Files Scanned at Source: 1373
    > Files Scanned at Destination: 101761
    > Elapsed Time (Minutes): 3.2678
    > Number of Copy Transfers for Files: 0
    > Number of Copy Transfers for Folder Properties: 0 
    > Total Number Of Copy Transfers: 0
    > Number of Copy Transfers Completed: 0
    > Number of Copy Transfers Failed: 0
    > Number of Deletions at Destination: 0
    > Total Number of Bytes Transferred: 0
    > Total Number of Bytes Enumerated: 0
    > Final Job Status: Completed
    > ```

    Please note that above command may take minutes / hours depending on the number and sizes of blobs present in source and destination containers. Also, once this command completes successfully, the same command can be run again to check if sync activity from source to destination has copied all the blobs.

5.  Use log files generated by the `az-copy` command internally, in case you need to identify any errors. For more information on how to access the log files, see the following documentation [Find errors and resume jobs by using log and plan files in AzCopy](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-configure).

    To understand how you could ensure that there are no performance issues during `az-copy` command execution, see [Optimize for large numbers of small files](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-optimize?toc=/azure/storage/blobs/toc.json#optimize-for-large-numbers-of-small-files).

6.  Once the migration is complete and after you verify that all the data has been copied to new container successfully, you must delete the old instances after deleting its bindings/service-keys.

7.  Rename the new instance with the old instance name, once the old instance is deleted. You may choose to delete the service-key for new instance as well.


