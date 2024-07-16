<!-- loio6ff2556fc21b4ae3808ae57686e489ad -->

# Guidance on building CF application that uses Object Store service

There are variety of use cases for using Object Store service. A Cloud Foundry application can be built to use Object Store service for supported object related operations.



To build an application using Object Store service, there are different aspects to consider before deciding upon the most appropriate approach. Some of those aspects are listed below:

-   Whether the service is to be used only on a specific IaaS.

-   Whether the service is to be used on two or more IaaSes

-   Whether the use cases are around only making basic object related operations like upload, download, delete objects.
-   Whether the use cases also require making use of IaaS specific features, that may be available on one while not on others or behave differently across different IaaSes


The approaches can be categorized mainly as follows:



<a name="loio6ff2556fc21b4ae3808ae57686e489ad__section_wvs_hnh_fhb"/>

## Using IaaS specific SDKs / APIs

Each IaaS provider has its own SDK available. If the service is to be used only on a particular IaaS, then IaaS specific SDK is simpler to use. The SDK also supports the IaaS related features. The SDKs provided by the IaaS providers are well built to help reduce the effort on client side. The IaaS providers themselves recommend using their SDKs. Due to the availability of the SDKs in varied languages, you can choose to develop applications with the programming language of your choice. Below are some links on how SDKs provided by respective IaaS providers can be used to build applications that use Object Store service.



[Using Amazon SDK in JAVA](https://help.sap.com/viewer/2ee77ef7ea4648f9ab2c54ee3aef0a29/Cloud/en-US/32517ae707c44ad48f635ea6bcbe271a.html)

[Using Azure SDK in JAVA](https://help.sap.com/viewer/2ee77ef7ea4648f9ab2c54ee3aef0a29/Cloud/en-US/f95653ea3ffe4eaeaf665c84d2edf8c1.html)

[Using GCP SDK in JAVA](https://help.sap.com/viewer/2ee77ef7ea4648f9ab2c54ee3aef0a29/Cloud/en-US/6248ccbf3e12417eab39aa207f80ed66.html)



<a name="loio6ff2556fc21b4ae3808ae57686e489ad__section_dhl_knh_fhb"/>

## Using open source client-side libraries

For building a CF application that needs to work across 2 or more IaaSes with only a basic set of object related operations, open source client-side libraries are useful. Such libraries abstract out the differences of various IaaS specific SDKs and provide a common set of methods for various operations, and hence help reduce effort and complexity around building and maintaining the application. You can develop the application once and get it deployed on various IaaSes.

JClouds [https://jclouds.apache.org/](https://jclouds.apache.org/) is one such open-source library available in JAVA.

Please refer the [tutorial](https://developers.sap.com/tutorials/cp-objectstore-mc-java-app.html) that describes with step by step instructions on using JClouds to build an application that works across various supported IaaSes.

You may also want to refer to a [sample application](https://github.com/SAP/cloud-objectstore-java-sample) built for reference. It demonstrates how JClouds \(an open-source JAVA client-side library\) can be used to accomplish the tasks at hand on AWS & GCP.

However, such open source libraries are not available in all popular programming languages. Also, such libraries may not support some advanced features for which IaaS based SDK/API have to be used. Further, as these libraries would have a lot of dependencies, managing the dependency updates could be challenging.

As these libraries are open-source projects, SAP doesn't hold responsibility of providing resolution for any issues that arise while using them.

