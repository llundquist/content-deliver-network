---

copyright:
  years: 2017
lastupdated: "2017-06-28"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Attach EdgeCast CDN account to SL Object Storage

## Enable your container(s) for public CDN access

### If you primarily wish to use the Control portal:

 1. Log in to the [Control portal](https://control.softlayer.com/), and navigate to **Storage** > **Object Storage**.
 
 2. Select the account then the Data center where your containers exist.
       **Note**: if you only have one object storage account, a DC list rather than an account list is displayed.
 
 3. Click once on a container you wish to make public.
 
 4. On the right-hand pane, click the **Enable CDN** checkbox.
 
 5. Repeat Steps 3. and 4. for each container you wish to make accessible via your EdgeCast account.
 
 6. Using the Steps 1. through 3., determine what the “AUTH_abcdef12-3456-7890-..." part of your account URL is and make a note of it.

### Alternatively, through the Object Storage API full API details available at [OpenStack](http://docs.openstack.org/api/openstack-object-storage/1.0/content/) and [SLDN](http://sldn.softlayer.com/reference/objectstorageapi):

 
  1. Authenticate against the Object Storage cluster where your containers exist. For the below examples let's assume your files are primarily stored in the DAL05 cluster, and we’ll use to curl get the information we need.
 An example authentication command with curl may look like this: <br/>
    ``curl -i https://dal05.objectstorage.softlayer.net/auth/v1.0 -H "X-Auth-User:youruser:yourusername" -H "X-Auth-Key:yourapikey"``
 
  2. In a successful auth response, you receive an HTTP 200 and receive a header called “X-Storage-Url”. Make a note of this URL as it is the base URL to your object storage account. For example: ``https://dal05.objectstorage.softlayer.net/v1/AUTH_[your token here]``.
 
  3. Also take note of the X-Auth-Token specified in the header, you will need it to identify yourself securely in the next API request. For illustration let's assume we were given one of “AUTH_tk12345”. <br/>
    **Note**: the full URL to a specific container like ``mycontainer`` would simply be appended to this URL, for instance: ``https://dal05.objectstorage.softlayer.net/v1/AUTH_[your token here]/mycontainer``
 
  4. Issue an HTTP POST against the container URL and include the ``X-Container-Read:.r:*"`` header, to indicate it can be read publicly — in this case by EdgeCast. For instance: ``curl -i -X POST https://dal05.objectstorage.softlayer.net/v1/AUTH_[your token here]/mycontainer -H "X-Auth-Token: AUTH_tk12345" -H "X-Container-Read:.r:*"``
 
  5. Repeat step 4 for each container you wish to make accessible via your EdgeCast account. In each case you should receive an HTTP 204 response.
    
## Add a Customer Origin and Edge CNAME at EdgeCast

1. Log in to the EdgeCast account portal.
2. In the menu, navigate to the platform/media type (HTTP large, HTTP small, etc.) you wish to connect to Object Storage and click **Customer Origin**.
3. Add a new Customer Origin with the following details:
    - Directory name: sl-dal05 (or whatever name you wish) 
    - Hostname or IP: http://dal05.objectstorage.softlayer.net:80
    - HTTP Host Header (should be filled in automatically): dal05.objectstorage.softlayer.net
    - Click the **Add** button to save the new origin.
4. From the same platform/media type menu, click **Edge CNAMEs**.<br/>
   **Note**: Adding a CNAME for the origin is not required if you wish to simply use the “based URL".
5. Add a new CNAME with the following details:
    - New Edge Cname:(or whatever name you wish)slcdn01.example.com
    - Points To: Customer Origin
    - Origin Directory: (the Customer Origin directory you added in step 3)
    - Directory Path: ``/v1/AUTH_[your token here]``<br/>
    **Note**: If you wish to tie this CNAME to a specific container on your account, also be sure to append ``/mycontainer`` to the end of this path.
    - Click the **Add button** to save the new CNAME.
    - Add the CNAME record to your domain’s DNS records to point to the **Points To** column on the resulting screen, omitting the ``http://`` portion.
    
    
## Linking to content in Object Storage via the CDN

- Determine Base URL:
   - If you added a CNAME for your Customer Origin, use that as the basis for your URL (for instance, http://slcdn01.example.com).
   - If you did not add a CNAME for your Customer Origin use the long form corresponding to your base Edgecast URL plus the above “Directory Path” component of what would have otherwise been used in a CNAME; for instance: ``http://wpc.ZZZZ.edgecastcdn.net/80ZZZZ/sl-dal05/v1/AUTH_[your token here]``
- Determine Container URL:
   - If you did not link the CNAME to a specific container, append the container name to the base URL formed in step 1. For instance, a base link to the ``mycontainer`` container for a CNAME would be ``http://slcdn01.example.com/mycontainer``.
- Determine Object URL:
   - Append the path within your container of the content you wish to link to. For instance, if you have an object within ``mycontainer`` called ``images/ghost.gif``, the CNAME based link would be “http://slcdn01.example.com/mycontainer/images/ghost.gif”.
- If you did link the CNAME to a specific container, the same steps apply above, but you only need to append the Object URL to the CNAME. For instance, if you set up a CNAME called and linked it to the ``mycontainer`` container, the object URL for the static.slcdn01.example.com ``images/ghost.gif`` object would then become ``http://static.slcdn01.example.com/images/ghost.gif``.
