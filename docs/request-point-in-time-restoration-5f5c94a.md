<!-- loio5f5c94a7749b494693eb427a914f38e5 -->

# Request Point-in-Time Restoration

You can request a point-in-time restoration on an instance if continuous backup was enabled for that instance.



<a name="loio5f5c94a7749b494693eb427a914f38e5__prereq_mk5_dss_pcc"/>

## Prerequisites

Continuous backups must have been previously enabled.



## Context

Two restoration options are available:

-   Entire bucket: Restore all objects inside the bucket.
-   Item level restore: Restore specific objects inside the bucket. You can restore up to 5 items.



## Procedure

1.  Create an SAP ticket with component BC-CP-CF-OSAAS.

2.  Provide the following details:

    **Point-in-Time Parameters**


    <table>
    <tr>
    <th valign="top">

    Parameter
    
    </th>
    <th valign="top">

    Description
    
    </th>
    </tr>
    <tr>
    <td valign="top">
    
    Instance ID
    
    </td>
    <td valign="top">
    
    Instance guid of the Object Store instance.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Region
    
    </td>
    <td valign="top">
    
    The region where the Object Store instance exists.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Restoration Timestamp
    
    </td>
    <td valign="top">
    
    The timestamp at which you want the instance to be restored, between 16 minutes and the backup retention period. With continuous backups, the backup is taken every 15 mins. So the restoration timestamp should not be earlier than 15 minutes.
    
    </td>
    </tr>
    <tr>
    <td valign="top">
    
    Location prefix
    
    </td>
    <td valign="top">
    
    The path prefix where restoration needs to be performed. \(This is applicable only with item level restore.\)
    
    </td>
    </tr>
    </table>
    

