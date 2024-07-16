<!-- loio9560c8616d244bf9803ea3f0b4246ef5 -->

# Instance Sharing

Object Store Service supports 'instance sharing' for all instances of 'objectstore' service, across all supported hyperscalers and environments.

> ### Note:  
> The capability is supported only for the 'standard' plan of 'object store' service. If you have instances of the deprecated plans \(s3-standard, azure-standard, gcs-standard\) and wish to enable instance sharing, you need to update those instances to the 'standard' plan. To know more about how to move to 'standard' plan, please refer to this [section](https://help.sap.com/docs/object-store/object-store-service-on-sap-btp/service-plan-update-to-standard).

For more information about this capability, please refer [Sharing and Unsharing Service Instances](https://help.sap.com/docs/authorization-and-trust-management-service/authorization-and-trust-management/sharing-and-unsharing-service-instances).



<a name="loio9560c8616d244bf9803ea3f0b4246ef5__section_jbg_tv5_m1c"/>

## How to enable instance sharing?

1.  The subaccount admin needs to make an 'objectstore' service instance shareable.
2.  A new service plan named reference-instance gets added.
3.  A developer can create a reference-instance pointing to the shared service instance.
4.  Apps can be bound to the reference-instance and can thus consume the shared service instance.

> ### Note:  
> To share or unshare a service instance, you must have subaccount-admin privileges.

Instance share using the Service Manager CLI: Use the following command:

```
smctl share-instance [name] --id [service-instance-id]
```

Instance share using the Service Manager API: This is done using the "Update a service instance" PATCH API with the following request body:

```
{
  "shared": true/false
}

```

Instance share using the SAP BTP Cockpit:

1.  Go to the subaccount *Overview*.
2.  In the left navigation pane, choose *Services* \> *Instances and Subscriptions*.
3.  Choose the *Instance* tab to view the instances provisioned so far.
4.  Choose the Actions \(*...*\) for the instance on which you want to enable instance sharing.
5.  Choose *Share Instance*.



<a name="loio9560c8616d244bf9803ea3f0b4246ef5__section_flt_3z5_m1c"/>

## How to create a reference instance of Object Store?

1.  Choose the environment \(Cloud Foundry or Kyma\) where you want to create a reference instance.
2.  While creating the reference instance, choose "reference-instance" plan of 'objectstore' offering/service and provide below parameters:

    ```
    {
        "referenced_instance_id": "",
        "selectors": {
            "instance_name_selector": "<shared-instance-name>",
            "plan_name_selector": "",
            "instance_label_selector": []
        }
    }
    
    ```

3.  This will provision a reference instance corresponding to the shared instance in the chosen environment. It is just a logical instance and acts as a 'pointer' to the original instance.
4.  Once the reference instance is created, you can create a binding for the newly created reference instance, and use the binding credentials to consume the originally shared instance.



<a name="loio9560c8616d244bf9803ea3f0b4246ef5__section_fpm_bfv_m1c"/>

## Important to know

1.  The limit of 5 bindings per service instance is still applicable. Therefore, the total number of service keys and bindings across the shared instance and all its reference instances cannot exceed the limit of 5.
2.  The option to choose 'reference-instance' as the plan, for creating a reference instance, is visible only when instance sharing is enabled by the subaccount admin on at least 1 of the instances.
3.  It is not allowed to unshare an instance if at least one reference instance is present for that instance. Only after the deletion of all the reference instances, we can unshare the original instance.

For more information on how to set up instance sharing on Object Store, see [Setting up instance sharing on Object Store](https://community.sap.com/t5/technology-blogs-by-sap/object-store-on-sap-btp-setting-up-instance-sharing-on-object-store/ba-p/13615448).

