<!-- loio26c3918cae3049a7bb3aaa3c0b4edb55 -->

# Service Plans and Entitlements

The following tables outline the service plan\(s\) and parameters use in the configuration of the service instance\(s\) exposed by the Object Store service on Infrastructure Providers:


<table>
<tr>
<th valign="top">

Service Plan

</th>
<th valign="top">

Environment

</th>
<th valign="top">

IaaS

</th>
<th valign="top">

Storage Class

</th>
<th valign="top">

Default Limits

</th>
<th valign="top">

Hard Limits

</th>
</tr>
<tr>
<td valign="top" rowspan="3">

standard

</td>
<td valign="top" rowspan="3">

Cloud Foundry, Kyma

</td>
<td valign="top">

AWS

</td>
<td valign="top">

AWS S3 Standard Storage

</td>
<td valign="top" rowspan="3">

-   Number of service instances per subaccount is 100 \(can be increased\)
-   In Azure, storage size is 5 PB per service instance \(can be increased\).



</td>
<td valign="top" rowspan="3">

Number of service bindings and service keys together: 5

</td>
</tr>
<tr>
<td valign="top">

GCP

</td>
<td valign="top">

GCS Standard Storage

</td>
</tr>
<tr>
<td valign="top">

Azure

</td>
<td valign="top">

Zone Redundant Storage

</td>
</tr>
</table>

Previous service plan\(s\) specific parameters:


<table>
<tr>
<th valign="top">

Service Plan

</th>
<th valign="top">

Environment

</th>
<th valign="top">

IaaS

</th>
<th valign="top">

Storage Class

</th>
<th valign="top">

Default Limits

</th>
<th valign="top">

Hard Limits

</th>
</tr>
<tr>
<td valign="top">

**azure-standard\***

\(Instances created until Q2 2021\)

</td>
<td valign="top">

Cloud Foundry

</td>
<td valign="top" rowspan="2">

Azure

</td>
<td valign="top">

Least Redundant Storage

</td>
<td valign="top">

5 PB storage per Cloud Foundry space \(can be increased\)

</td>
<td valign="top" rowspan="2">

Number of service bindings and service keys together: 5

</td>
</tr>
<tr>
<td valign="top">

**azure-standard\***

\(Instances created after Q2 2021\)

</td>
<td valign="top">

Cloud Foundry, Kyma

</td>
<td valign="top">

Zone Redundant Storage \(container name has ‘zrs’ suffix\)

</td>
<td valign="top">

5 PB storage per service instance \(can be increased\)

</td>
</tr>
</table>



> ### Note:  
> The “Standard” service plan unifies the delivery of the service in all hyperscalers, simplifying all the existing commercial plans. All existing plans capabilities are now under Object Store's "standard" plan, providing the same service functionalities, customers should use the ''standard'' service plan for all new Object Store instances.
> 
> \*The "azure-standard", "s3-standard" and "gcs-standard" service plans were removed from the list of Eligible Cloud Services as of 15.01.2024. Existing instances will not be impacted and will be available until the end of the current subscription term. They will not be available for renewal terms that begin after the removal date.
> 
> For information on updating your instances to the ‘Standard’ plan please refer to [Service Plan update to 'standard'](service-plan-update-to-standard-d891fb7.md)

> ### Note:  
> Please be note that the cloud service comes with a restriction on the monthly requests \(api\_calls\) number, for more information please check SAP Business Technology Platform Service Description Guide, [part of the contractual terms and is available via SAP Trust Center Agreements](https://www.sap.com/portugal/about/trust-center/agreements/cloud/cloud-services.html?sort=latest_desc&search=Platform%20Service%20Description%20Guide).
