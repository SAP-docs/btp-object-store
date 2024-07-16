<!-- loio9d41a24262fd4a62b8b7b64a643f5eab -->

# Object Level Tagging

With Generated SAS you can set/get/delete tags on blobs.

Get blob tag list

> ### Sample Code:  
> ```
> az storage blob tag list --blob-endpoint <blob_primary_endpoint> --container-name <container_name> --name <blob_name> --sas-token <sas_token>
> ```

Set blob tags

> ### Sample Code:  
> ```
> az storage blob tag set --blob-endpoint <blob_primary_endpoint> --container-name <container_name> --name <blob_name> --tags tag2=value2 tag1=value1 --sas-token <sas_token>
> ```

Upload blob with tags

> ### Sample Code:  
> ```
> az storage blob upload --blob-endpoint <blob_primary_endpoint> --container-name <container_name> --file <file_path> --name <blob_name> --tags tag1=value1 --sas-token <sas_token>
> ```

