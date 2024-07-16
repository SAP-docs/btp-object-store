<!-- loiodab81b685105424ca84d74406d244560 -->

# Data Protection and Privacy

Governments place legal requirements on industry to protect data and privacy. We provide features and functions to help you meet these requirements.

> ### Note:  
> SAP does not provide legal advice in any form. SAP software supports data protection compliance by providing security features and specific data protection-relevant functions, such as simplified blocking and deletion of personal data. In many cases, compliance with applicable data protection and privacy laws will not be covered by a product feature. Definitions and other terms used in this document are not taken from a particular legal source.

The following sections provide information about the Object Store service. For the central data protection and privacy statement for SAP BTP, see [Data Protection and Privacy](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/7e513d31704a4a87831191e504ca850a.html)



<a name="loiodab81b685105424ca84d74406d244560__section_cxt_tv5_fcb"/>

## User Consent

We assume that software operators, such as SAP customers, collect and store the consent of data subjects, before collecting personal data from data subjects. A data privacy specialist can later determine whether data subjects have granted, withdrawn, or denied consent.

The Object Store service does not provide any support for collecting and storing the consent of data subjects for applications built on SAP BTP. It is the responsibility of your developers to provide such support.

No customer personal data must be used in any other data fields \(other than content of objects within S3 buckets\) like object key, metadata, tags etc. This is because these fields are not intended for storing personal data.



<a name="loiodab81b685105424ca84d74406d244560__section_k2f_r3h_fdb"/>

## Read-Access Logging and Change Log

Audit logs are available for all broker related operations of Object Store \(like create service, bind service, unbind service, update service, create service-key, delete service\) on all SAP supported infrastructures.

In case of AWS, Microsoft Azure and GCP, a CF application that is bound to an ObjectStore instance, gets a direct URL to the underlying Object Store \(S3/Azure/GCS\), along with relevant access to perform object related operations \(like upload, download, delete objects\) directly. Therefore, the ObjectStore-as-a-Service cannot audit log any of the object related operations.

The Object Store service doesn’t deal with any personal data. However, the service has no control over the kind of data that is written to an Object Store \(S3/Azure/GCS\).

To extract the audit logs, you need to create a BCP ticket against Object store in the component BC-NEO-CF-OSAAS. The audit log data stored for your account will be retained for 30 days, after which it will be deleted.



<a name="loiodab81b685105424ca84d74406d244560__section_nsx_cx5_fcb"/>

## Erasure

When handling personal data, consider the legislation in the different countries where your organization operates. After the data has passed the end of purpose, regulations may require you to delete the data. However, additional regulations may require you to keep the data longer. During this period you must block access to the data by unauthorized persons until the end of the retention period, when the data is finally deleted.

You can delete your Object Store service, and therefore, all the data stored in your databases. To do so, navigate to your sub account using the procedure [Navigate to Global Accounts, Subaccounts, Orgs, and Spaces in the Cockpit](https://help.sap.com/viewer/65de2977205c403bbc107264b8eccf4b/Cloud/en-US/5bf87353bf994819b8803e5910d8450f.html) and delete the service from the *Overview* page.

If you want to delete the objects from S3 buckets or containers, you can do so by making object delete calls. If you want to delete the bucket or container, then you can make a `cf delete-service` instance call. The time taken to delete the container/S3 bucket depends on the number of objects present in the container/S3 bucket.

ObjectStore-aaS doesn’t support any backup solution as there is no out-of-the-box backup feature provided by any of the supported hyperscalers. ObjectStore is itself used to store data backups.

However, the supported hyperscalers do provide replication of data across multiple availability zones/locations. The replicas get deleted when the corresponding object deletion happens. Please refer [Region](https://help.sap.com/viewer/2ee77ef7ea4648f9ab2c54ee3aef0a29/Cloud/en-US/8c20208a0891482b90bc6192633239b8.html) section here for further information on the data replication.



<a name="loiodab81b685105424ca84d74406d244560__section_fgx_xv5_fcb"/>

## Glossary


<table>
<tr>
<th valign="top">

Term

</th>
<th valign="top">

Definition

</th>
</tr>
<tr>
<td valign="top">

**Consent** 

</td>
<td valign="top">

The action of the data subject confirming that the usage of his or her personal data shall be allowed for a given purpose. A consent functionality allows the storage of a consent record in relation to a specific purpose and shows if a data subject has granted, withdrawn, or denied consent.

</td>
</tr>
<tr>
<td valign="top">

**Deletion** 

</td>
<td valign="top">

Deletion of **personal data** so that the data is no longer available.

</td>
</tr>
<tr>
<td valign="top">

**Personal data** 

</td>
<td valign="top">

Any information relating to an identified or identifiable natural person \("data subject"\). An identifiable natural person is one who can be identified, directly or indirectly, in particular by reference to an identifier such as a name, an identification number, location data, an online identifier or to one or more factors specific to the physical, physiological, genetic, mental, economic, cultural, or social identity of that natural person

</td>
</tr>
<tr>
<td valign="top">

**Retention period** 

</td>
<td valign="top">

The period of time between the end of the last business activity involving a specific object \(for example, a business partner\) and the deletion of the corresponding data, subject to applicable laws. The retention period is a combination of the residence period and the blocking period.

</td>
</tr>
<tr>
<td valign="top">

**Sensitive personal data** 

</td>
<td valign="top">

A category of personal data that usually includes the following type of information:

-   Special categories of personal data, such as data revealing racial or ethnic origin, political opinions, religious or philosophical beliefs, trade union membership, genetic data, biometric data, data concerning health or sex life or sexual orientation, or personal data concerning bank and credit accounts.
-   Personal data subject to professional secrecy
-   Personal data relating to criminal or administrative offenses
-   Personal data concerning insurances and bank or credit card accounts



</td>
</tr>
</table>

