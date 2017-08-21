---

copyright:
  years: 2017
lastupdated: "2017-07-12"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Enabling the SSL Option for CDN

SoftLayer offers Content Delivery Network (CDN) options via EdgeCast. The service includes the ability to deliver content using HTTPS or Secure Socket Layer (SSL) connections. 


## Considerations

There are two options for SSL with CDN:

- *SoftLayer shared certificates* are wildcard certificates that are valid for all CDN-related URLs. The SoftLayer certificate is valid for all URLs that end with cdn.softlayer.com.

- *Customer-specific certificates* are certificates provided by the customer that are installed on the CDN server. They allow customer-specific URLs to be protected with SSL. Customer-specific certificates require manual processes and have significant yearly costs associated with them.

SoftLayer CDN accounts are provisioned with SSL disabled. Once SSL is enabled, they use the SoftLayer wildcard SSL.


## Pre-requisites  

In order to enable SSL with your CDN, you need to have active Object Storage and CDN accounts. Make a note of your Object Storage and CDN account IDs if you already have them.

You will need to order an Object Storage and or CDN account if you do not currently have these account IDs. After your Object Storage account has been provisioned, you will have access to the same account ID on all Object Storage clusters.

When ordering your CDN account, use the “CDN Pay as You Go Bandwidth” option. Your CND account ID will be assigned to you. For our example, our CDN account ID is 12B17.
Activating CDN SSL with Object Storage

CDN is enabled for regular HTTP traffic. Follow the steps below to enable CDN with SSL on your CDN account:

1. Open a browser window, enter control.softlayer.com, and log in.

2. Click **Support**, **Add Ticket**, and enter the following information:
 <table><tbody>
 <tr><th>Field</th><th>Value</th></tr>
 <tr><td>Subject</td><td>CDNLayer question</td></tr>
 <tr><td>Title</td><td>Please upgrade CDN account to allow SSL with shared Certificate</td></tr>
 <tr><td>Details</td><td>Please upgrade CDN account to allow SSL with shared Certificate</td></tr>
 </tbody></table>

3. Create a container on your Object Storage account while the ticket is being processed – click **Storage**, **Object Storage**, and select your ObjStore account. Select a **Cluster** (data center), and click the **Add Container** button. We created a container named static-content for our example. 

4. Click on the container name and click the Enable Static Site checkbox under Status Site Access. All the content of the container will display as a URL below the checkbox. <br/> ![Container description panel](/images/cdn_fig1.png)

5. Open a new ticket - once the previous ticket has been processed - requesting that the Object Storage URL be bound to your CDN account by clicking **Support**, **Add Ticket**.
   Be specific about which CDN and URL are to be bound. Below is our ticket request for our example using the information in Figure 1:
 <table><tbody>
 <tr><th>Field</th><th>Value</th></tr>
 <tr><td>Subject</td><td>CDNLayer question</td></tr>
 <tr><td>Title</td><td>Please BIND Object Storage URL with CDN account</td></tr>
 <tr><td>Details</td><td>Please bind the Object Storage URL https://dal05.objectstorage.softlayer.net/v1/AUTH_30f2b8a1-cfa8-4c22-8347-caec1bd0c199/static-content to the CDN account 12B17.</td></tr>
 </tbody></table>

6. Upload your files to the container while the ticket is being processed by clicking on your container name and click Upload Files and Folders.
   Files up to 20MB can be uploaded directly from the customer portal using Actions, Add File on the container’s description panel. We added the file sla.pdf for our example.  

7. Manage the file's CDN properties, after it has been uploaded, by clicking on its icon (see Figure 2). Clicking on the name will download the file. </br>
![Figure 2: File within an Object Storage panel](/images/cdn_fig2.png)

8. Use the panel to Prime Cache (i.e., send the file to the CDN) and set the Time to Live (TTL) (i.e., how long the CDN must hold the file).

## Testing

Access the file one of several ways once you have set it up:

- Directly on the Object Storage using `HTTPS: https://dal05.objectstorage.softlayer.net/v1/AUTH_30f2b8a1-cfa8-4c22-8347-caec1bd0c199/(container name)/(file name)`

- Through the CDN without SSL (using the URL from the container panel): `http://12b17.http.dal05.cdn.softlayer.net/(container name)/(file name)`. <br/> Note that the CDN ID (12B17) is part of the URL.

- Through the CDN with SSL: `https://12b17.https.cdn.softlayer.net/(container name)/(file name)`. <br/>The CDN ID is also part of the URL.

All of the access options will work if everything is setup correctly. Direct access to the Object Storage will not use any of the CDN points-of-presence (it is best to test that the files are really there before testing the CDN).

## Final Considerations

Enabling SSL on your CDN may be counterproductive because of the increase of the connection time due to the SSL handshake. It is advisable to benchmark your load time to see if the CDN still improves the overall user experience. You can always revert back to non-encrypted connections.

If the content you are distributing from the CDN requires proof of origin, you can still use normal HTTP connections in combination with digitally signing the files. The combination of connections and signed files is used extensively for the distribution of binaries all over the Internet. The object signatures must be checked upon download to make sure that the file was not tampered with during the transaction.
