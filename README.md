# Welcome to the Cookdown Discovery and Mapping Payload Store!

The files in these directories contain the payloads that the [Cookdown Discovery](https://cookdown.com/discovery/) and [Cookdown Mapping](https://cookdown.com/service-mapping/) solutions uses to populate your ServiceNow CMDB with CIs and Services. They are in the correct format for ServiceNow&#39;s Identification and Reconciliation Engine&#39;s public API to accept once the Cookdown Discovery product has parsed them in your environment, replacing the parameterised keys in them with the actual values from each SCOM object in the class they are for.

Before getting going, please read this document as there are some important points to consider before using them, that if not planned for will result in duplicate CIs or undesired results in your ServiceNow instance

## What these payloads are good for

- Greenfield environments with no other CMDB discovery sources
- CMDBs that discover from ServiceNow&#39;s own discovery tool – these payloads will result in CIs compatible with those from ServiceNow Discovery. They have been built around compatibility with ServiceNow&#39;s own discovery tool
- ServiceNow&#39;s out of the box Identification and Reconciliation rules – if a payload requires any Identification and Reconciliation rule changes from default it will be noted in the readme within each file or within this readme
- Getting inspiration for your own custom payloads

## What these payloads are not good for

- CMDB population without the Cookdown Discovery product – they wont do anything without it
- Highly customized CMDBs – if there are CMDB fields made mandatory that we have not planned to populate, discovery will fail
- ServiceNow instances with custom Identification and Reconciliation rules – these payloads have been designed around compatibility with CIs from ServiceNow&#39;s own discovery product. Please review the payload(s) you would like to use before pushing CIs with them to avoid duplicate CIs when used with your custom/modified rules
- CMDBs which use ServiceNow&#39;s SCCM discovery tool – these payloads use the &quot;correlation\_id&quot; field for storing the SCOM object ID of each discovered CI into ServiceNow. The SCCM discovery tool uses this same field so avoid the SCCM correlation ID being overwritten or duplicate CIs, simply change the correlation\_id field in these payloads for another field to make them compatible with the ServiceNow SCCM discovery tool

## Other important considerations

The &quot;Correlation\_id&quot; field is used to store the SCOM object ID with each CI. If you have another discovery tool that uses this same field (like the SCCM discovery tool from ServiceNow) then use a different field for the SCOM object ID.

Do not use payloads from this store without first testing what they will do in your own environment or you risk creating duplicate CIs or unusual relationships in your CMDB.

## Service Mapping and store payloads

Some payloads (those with &quot;Y EAs&quot; in their name) are designed to push mapped applications from SCOM into ServiceNow and to relate the CIs they create to them, or example the SQL database payload created SQL databases and relates them to the mapped application. These payloads push applications into the &quot;Application Service&quot; CI class (table cmdb\_ci\_service\_discovered). If this is not the desired type of service simply change the CI class that is mentioned in each payload.

Payloads whos name contains &quot;Y EAs and Y Groups&quot; will create an Application Service for both the mapped application and the groups displayed in the Squared Up VADA UI – pushing up the groups is visually pleasing when viewing the created Application Services in ServiceNow, but is not ServiceNow best practice.

Out of the box, ServiceNow ships with no Identification rule for Business/Application Services, so for mapping payloads to work an Identification Entry needs to be created, identifying apps as unique based on &quot;name&quot; and &quot;correlation\_id&quot; (or whichever field you choose to store the SCOM object ID in your CMDB)

Full documentation on Cookdown Discovery and Mapping can be found at [http://support.coookdown.com](http://support.coookdown.com)

## Classic vs Liquid payloads

There are two formats, 'Classic' and 'Liquid'. Each defined in their own top level folder. If you are using a recent version of our product you should use the Liquid format. To use classic payloads with the liquid engine, you normally just need to swap out the keys in use with ones in the new format.