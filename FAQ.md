---

copyright:
  years: 2017
lastupdated: "2017-07-31"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# CDN FAQ

## What is a Content Delivery Network (CDN)?

A Content Delivery Network (CDN) is a system of Bare Metal Servers using advanced software for organizing, storing, and streaming website content for the express purpose of optimizing the flow of the content to end-users. It distributes the content to multiple, geographically diverse nodes and then serves the content from whichever node is closest to the end-user, minimizing packet travel and increasing speed and efficiency. There are two types of CDNs—virtual networks that connect end-users directly to the Bare Metal Server and hybrid networks that combine CDNs with peer-to-peer networks.

## Which Type of CDN Should I Use?

Typically, sites with heavy traffic loads will benefit from an origin pull CDN, as content is pulled from the host server and users can pull cache content from the CDN. On the other hand, users can benefit from a PoP pull CDN by controlling what gets uploaded to a CDN FTP, when it expires, and what it is updated making it very efficient to manage. Regardless of the type of CDN chosen, deploying a CDN means getting content to users faster and more efficiently.


## How Do I Stream Movies or Other Media?
There are a variety of methods to stream content via the CDN:

  ### HTTP Progressive
  HTTP Progressive download uses the HTTP protocol to stream archived media content. As a result, it cannot take advantage of the security features that are available with the RTMP protocol, such as encryption and SWF verification. Additionally, the entire video is downloaded to a user’s computer. As a result of all of these factors, HTTP Progressive Download is more susceptible to piracy than either Live StreamCast or On-Demand Streaming. This method can be used with Flash video or Windows Media files.
 
  ### Windows Live Streamcast
  This method allows you to distribute a live video stream to the CDN and then to browser clients. You can set up the stream to be push or pull, meaning that either the server will “push” the video stream to the CDN for download, or the CDN will “pull” the content from your server when requests for the stream are needed.

  ### Windows On Demand Streaming
  The first step in this process is for a client to request on-demand content from our CDN. This type of request occurs when a media player points to a stream using a player URL that references on-demand content stored on a CDN origin server. (This is not your server, but rather a server on the CDN that has the media uploaded to it previously.)

When a client requests on-demand content, a check is performed to find out whether the requested content has already been cached at the POP closest to your client. If it is already there, then the on-demand content is immediately served up to that client. This allows those clients to enjoy even faster on-demand streaming. If the requested Windows media content is not found, the second step for serving on-demand content is for the POP closest to the client to retrieve the requested Windows media content from the CDN origin server.

If the requested on-demand content has not been cached, then it will be delivered from the CDN origin server to the POP closest to the client. The stream will be delivered to this POP by leveraging our worldwide network. This allows us to bypass traditional Internet communication routes, which ensures the efficient transmission of your Windows media content and reduced bandwidth load on your server. By default, on-demand content will be cached on that POP. This allows future requests from the region served by this POP to bypass data retrieval from the CDN origin server.

Image files, documents and other static content that you wish to make available can be done so by simply linking to it on your web site. For example, if you wish to put images on the CDN you would use the following code to display it on your site:
``<image src="http://http.cdn.com/%3Cusername/img.jpg alt=”my image” />`` This would direct users’ browsers to download the image from the CDN as opposed to directly from your servers.

## Why Am I Getting a NO DATA Error When Uploading Files to the CDN?
The error “No Data” when using the Java applet to upload a file greater than 20MB is due to the file size limitations we have in place on the Java applet. Use Proxy FTP to work around this limitation.

Instructions for accessing FTP credentials for CDN may be found here. Please note that users may only access the Proxy FTP from a Bare Metal Server on our network.


## Can I Upload Files to CDN via FTP or SCP?
Absolutely, you may upload files via FTP.  Unfortunately, you may not use SCP at this time.

Access to the FTP service can be done either through the MCC FTP java applet or to the CDN directly. The login details and specific FTP server information can be found in the MCC panel, under Media Manager > FTP menu.


## How Many Nodes Does CDN Use?
CDN currently delivers content across 24 nodes (and growing) around the globe, including the Americas, Europe and Asia. This provides geographic diversity and the ability to deliver content from some of the largest Internet peering points in the world. SoftLayer and its partner, Edgecast, will continue to add new nodes to CDN to expand the reach and capabilities of the service.

## Can a User Have CDN and StorageLayer Permissions Granted but be Prohibited from Accessing Object Storage?

If a user has the Manage CDN Account, Manage CDN File Transfers and Manage StorageLayer permissions granted, the user automatically has access to Object Storage, as well. At the current time, granting access to CDN and StorageLayer while prohibiting access to Object Storage, or vice versa, is not an option.

## How Can I Monitor How People Are Using My Online Content?

The MCC control panel contains a variety of graphs available under the Reports menu. Summaries of traffic usage across all CDN types can be displayed, along with cache hit/miss ratios, current amount of storage being used and other data. Access logs are generated by the CDN are available in the Media Manager interface and can also be retrieved via FTP.

## What File Formats Does CDN Support?
SoftLayer’s CDN Supports Windows Media for streaming files. SoftLayer’s CDN also supports a wide array of encoding formats for downloading or caching media—including Windows Media Player, DivX, H.264, Move Media Player, Microsoft Silverlight, QuickTime, MP3, RealSystem G2, RealPlayer, Real Networks, HTML, TXT, GIF, JPG, and PDF.


## How Do I Stream Movies or Other Media with CDN?
To stream flash content you will need to use a flash player. Flash files that end in .swf generally have the player pre-compiled into them and aren’t considered streaming files. Flash content that can be streamed generally ends in .flv and requires a flash player. There are many open source flash players available for use that are free and can be used with very little code.

Windows media files are generally streamed in the formats of WMV of ASF files. To use them in your website you would need to “embed” them with the object.

Image files, documents and other static content that you wish to make available can be done so by simply linking to it on your web site.

## How Do I Upload Files to CDN?

The CDN currently allows uploading and managing files via Origin Pull. Origin Pull is a method of pulling data directly from your local web server and caching it on the CDN in the HTTP folder.

## How Does Origin Pull Work?
Origin Pull is the method of transferring data to the CDN automatically from a webserver as opposed to manually uploading the content. This method of uploading data to the CDN can be used for HTTP and on demand Windows Media content. Once the initial configuration is completed, the content will become available to the CDN by simply requesting the CDN URL associated with that content.

For example:

Edge CDN URL can point to a Bare Metal Server to obtain content. The Edge CDN URL will be http://SLXXX.cdn.softlayer.net, and the Origin URL will be http://myserver.com.

The IMG tag will tell the client to retrieve the picture.jpg image from the Edge CDN rather than directly to the Bare Metal Server. If the image is not already stored on the CDN cache, then it will go to your Origin URL, retrieve the content from the images directory, and then display it while caching the image on the CDN server. On the next request, the image will be served directly from the CDN rather than the Bare Metal Server and subsequent page loadings will be much faster.

With Origin Pull, the CDN determines if content will need to be pulled from the Bare Metal Server via the “Cache-Control” headers configured on the webserver. The CDN will honor most standard Cache-Control options such as max-age, proxy-revalidate, must-revalidate. Please note that the use of the ”private” and “no-cache” option in the Cache-Control headers will result in the CDN pulling a new version of the content for each request it receives as the headers will instruct it not to cache that content.

We recommend not setting your max-age to less than 5 to 10 minutes as this will put excessive load on your webserver and result in less optimal performance. Be aware that if content on the webserver has been updated, each POP will continue to serve the old cached version until that cache is purged or the cache on the POP expires. If no max-age header is set, the default max-age of 24 hours will be used.

## What Is Origin Pull and How Does It Affect My CDN Account?

With Origin Pull, the requested content is pulled from your origin servers as needed and then delivered to your customers. You can set rules for how long content is considered fresh and the CDN will automatically track this and only request an update when necessary. This helps reduce the bandwidth and overhead on the web server.

   **Note**: Your contents may not exactly be updated at the cache lifetime you specified in the HTTP header because the CDN has clouds of servers all over the world and requests can be made to any of those servers. The cache control on each CDN server is independent from each other.

If attempting to use Origin Pull when the web server is offline or not functioning, the CDN will continue to display the data it already has so long as the cache lifetime hasn’t expired and will not be able to update it until your web server is functioning properly again. This means that you will get outdated or partial content on the CDN if your web server isn’t fully functional.

Origin Pull is not designed to be accurate 100% of the time. The cache-control options are an approximate value and are generally accurate to within 10 minutes.

## What are Some Example Configuration Changes for Origin Pull on an Apache Web Server?

Here are some example Apache Web Server configuration options that will enable cache-lifetime headers:<br/>
- For Apache, mod_expires and mod_headers handle cache control through HTTP headers sent from the Bare Metal Server. 
- For Apache/1.3x, enable the expires and headers modules by adding the following lines to your httpd.conf configuration file.

  `LoadModule expires_module     libexec/mod_expires.so`<br/>
  `LoadModule headers_module     libexec/mod_headers.so`<br/>
  `AddModule mod_expires.c`<br/>
  `AddModule mod_headers.c`<br/>
  `...`<br/>
  `AddModule mod_gzip.c`<br/>
  Note that the load order is important in Apache/1.3x, mod_gzip must load last, after all other modules.
  
- For Apache/2.0, enable the modules in your httpd.conf file like this.

  `LoadModule expires_module modules/mod_expires.so`<br/>
  `LoadModule headers_module modules/mod_headers.so`<br/>
  `LoadModule deflate_module modules/mod_deflate.so`<br/>
  
  mod_deflate is the native compression module in Apache/2.0 (although mod_gzip does a better job of handling wayward browsers). In this case, the load order does not matter, as Apache/2.0 handles this for you.
  
  ETag (Entity Tag) may be problematic if you have clustered Bare Metal Servers. See http://en.wikipedia.org/wiki/HTTP_ETag
  
  `Header unset ETag`<br/>
  `FileETag None`<br/>
  Files in this directory will not be cached
  
  `Header Set Cache-Control "max-age=0, no-store"`<br/>
  Files in this directory will be cached for 5 minutes.
  After 5 minutes, CDN server will check if the contents has been modified or not.
  If not modified, Apache will send 304 "Not Modified" header.
  If modified, the contents will be updated.
  
  `Header set Cache-Control "max-age=300, must-revalidate"`<br/>
  Files in this directory will be cached for 1 day.
  After 1 day, CDN server will check if the contents has been modified or not.
  If not modified, Apache will send 304 "Not Modified" header.

  `Header set Cache-Control "max-age=86400, must-revalidate"`<br/>
  Files in this directory will be cached for 1 week.
  After 1 week, CDN server will check if the contents has been modified or not.
  If not modified, Apache will send 304 "Not Modified" header

  `Header set Cache-Control "max-age=604800, must-revalidate"`<br/>
  The above Directory directives require the full path to the directory on the server, not the subdirectory of the URL. For example, if your domain content is stored in /var/www/mydomain and you wish to set cache-control options on your ‘images’ directory, you would need to specify /var/www/mydomain/images in the Directory directive.


## What is CDN HTTP Small Object?
HTTP Small Object is a method of caching objects on our Content Delivery Network (CDN). This method honors all HTTP 1.1 cache control rules; however, HTTP Small Object caches objects up to 300KB in size and is not enabled for streaming. Objects cached using HTTP Small Object may only be reached using their HTTP or HTTPS URL. Objects cached on servers devoted to HTTP Small Object are retrieved quicker than our traditional CDN offering - they are stored in the server's memory as opposed to being stored on a disk, making them more readily accessible by our systems.


## How Do I Know If I Should Use HTTP Small for My CDN Needs?
Most users primarily utilize our standard (HTTP Large Object) CDN offering. Files are easily cached on the standard platform and there are no size limitations to objects stored and delivered with the standard offering. HTTP Small Object should be used when speed is a necessity, the file in question is 300KB or less in size, and the functionality available in our standard CDN offering is not required for delivery of the file (i.e. streaming content). If the file is unable to meet these parameters, use our standard CDN option.


## Why Should My Company Outsource the Use of a CDN and Not Build Its Own Infrastructure?

Using CDN reduces your internal overhead by relying on IBM Bluemix’s servers designed specifically for the task of streaming video and content. Rather than building infrastructure from the ground up, we offer several clustered systems in geographically diverse locations. The end result is having the work of one server spread over hundreds. Finally IBM Bluemix’s partner for CDN (Edgecast) has provided us with a 100% SLA agreement meaning your content is in safe and dependable hands.


## Can I Rename a File on CDN?

Renaming a file on CDN is not permitted as there isn’t a way to track those changes on the nodes around the world. If you wish to rename a file you have already uploaded to CDN you will need to upload the new renamed file and then purge the old file.


## Is CDN integration Available on my Object Storage Account?

Yes, CDN integration is a standard feature on all Object Storage accounts.  All interactions with the CDN portion of your account must be managed through SoftLayer’s API and CDN integration must be activated on your account prior to its use.  For more information on interactions with the CDN portion of your Object Storage account, refer to the [Object Storage CDN](http://sldn.softlayer.com/reference/Object-Storage-CDN) reference page of the SLDN.

## Does SoftLayer Partner with Another Company to Deliver the CDN?

SoftLayer partners with Edgecast for CDN because they are a consistent industry leader in Internet content distribution technologies.

## How Can I Monitor How People Are Using My Online Content?

The MCC control panel contains a variety of graphs available under the Reports menu. Summaries of traffic usage across all CDN types can be displayed, along with cache hit/miss ratios, current amount of storage being used and other data. Access logs are generated by the CDN are available in the Media Manager interface and can also be retrieved via FTP.

## How Is CDN Billed to My Account? 

CDN usage is a pay-as-you-go service, meaning that it is metered and billed in arrears. It is available both as standard bandwidth, with optional SSL for an additional charge.

Prices shown on softlayer.com are for our large object offering, which is available in a number of geographic regions. For customers looking for small object delivery or CDN connectivity throughout many locations in Asia Pacific, we offer unique packages for Small Object and Asia Premium. To order these packages, or to learn more about additional CDN services available through SoftLayer, please contact our Sales team.

## How Does CDN Determine Which Node to Use?

CDN monitors an end-user’s location as well as network traffic and chooses which node will deliver the content with the least latency. It begins by analyzing the node with closest geographic proximity to the end-user. If the node’s performance will be compromised due to hardware, bandwidth traffic, or other issues, CDN will direct content around the point of failure to maintain ultimate end user experience.

## How Does CDN Work?

CDN is powered on two levels. The underlying level is the network infrastructure—a global Internet backbone connecting various nodes on multiple continents. This allows content to be delivered from an optimal proximity to the end-user. The second level is the operating software which directs content between the nodes and maintains load balancing and content integrity.

## How Do I Begin Using CDN?

Users with an existing account can easily add CDN as a service in the Customer Portal from the [CDN screen](access-cdn-screen.html). New customers may order the service on the [CDN page](https://www.ibm.com/cloud-computing/bluemix/content-delivery-network) on ibm.com.

## How Do I Enable Origin Pull on My CDN Account?

Origin Pull is enabled by default.

## How Do I Know If I Should Use HTTP Small for My CDN Needs?

Most users primarily utilize our standard (HTTP Large Object) CDN offering. Files are easily cached on the standard platform and there are no size limitations to objects stored and delivered with the standard offering. HTTP Small Object should be used when speed is a necessity, the file in question is 300KB or less in size, and the functionality available in our standard CDN offering is not required for delivery of the file (i.e. streaming content). If the file is unable to meet these parameters, use our standard CDN option.


## How Much Faster Is CDN Compared with Standard Internet Content Delivery?

The difference in delivery speeds between CDN and standard Internet delivery varies based upon network conditions. The strength of CloudLayer CDN lies in its ability to maintain reliable, consistent speed of delivery regardless of external network conditions. When standard Internet delivery is at its slowest, the content delivered over CDN will remain virtually unaffected. CDN also creates levels of redundancy for content distribution. If a single CDN node is out, the content is simply served from another location, thus reducing website outages and improving overall performance. CDN will essentially take the workload and bandwidth of any one server and distribute it amongst hundreds of servers worldwide, ensuring your end-user the best possible performance.


## How Reliable is CDN?

CDN is substantially more reliable for content delivery than standard unmonitored Internet delivery. By reducing stress on the host server and distributing content over a network of nodes, information can be stored securely and delivered consistently. Particularly for large file downloads or streaming media where latency can create interruptions, CDN helps content arrive rapidly and without jitters, excess buffering, or service interruptions.

## How Soon Is My Content Available Once Transferred to the CDN? 

After uploading a file to CDN it is immediately stored on a central database node. The content is then delivered to CDN nodes around the world as it is requested. It is important to remember the first time content is requested there will be minimal latency as the file is moved to the local server. Subsequent requests for that content will then be readily available for anyone near that location and the full capabilities of CDN will be utilized in respect to speed and quality. Another important note, with the caching content system, the files in each of there respective nodes around the world will be refreshed approximately every two days therefore the content will have to be requested and re-cached in a server local to the end-user for others in the same location to experience the benefit.

## What Are the Advantages of Using CDN over Standard Internet Content Delivery?

CDN delivers content more efficiently than standard Internet content delivery, letting businesses meet the growing demand for rich, online media that require large bandwidths.

Standard Internet delivery sends content data over general Internet routes from the host server’s location to the end-user’s location. This takes into account neither the host server’s proximity to the end-user, nor possible traffic jams between the two. CDN, however, moves the content from the host server to a node that is geographically closer to the end-user. This avoids potential network congestion and decreases latency, increasing delivery speed and providing consistent and reliable file transfer times. In addition, as a solution created specifically for content delivery, CDN includes tools that provide more content management and delivery control, helping with content monetization.

## What Are the Key Advantages of CDN? 

- ***Cost-Effective Scalability*** - Pay-as-you-go bandwidth accommodates changes in user demand without excess capacity.
- ***Performance-Neutral Growth*** - Spreading content delivery over multiple servers throughout the cloud ensures that increased demand for content does not slow down or compromise delivery.
- ***Secure Content Management*** - Secure, streamlined tools for managing content and content monetization protects digital rights and maximizes return.
- ***Geographic Reach*** - Pushing content to nodes around the world optimizes the speed and reliability of content delivery to end-users regardless of location.
- ***High-Quality Content & Media Rich Web Sites*** - Optimizing data and content delivery allows web sites to include richer, more creative content without sacrificing performance.

## What Is the CDN Asia Premium Package?

The CDN Asia Premium package is available on all new and existing CDN Accounts. This offering extends the Content Delivery Network to points of presence (POPs) in the following locations:

- Hong Kong
- Osaka
- Singapore
- Tokyo

The Asia Premium package provides access to all of EdgeCast's CDN POPs located in the Asia Pacific (APAC) Network and offers premium route preferences. It provides faster responses and access times to content requested from the APAC Region.

Existing users may create a ticket to request the Asia Premium package for CDN. For additional questions concerning the Asia Premium Package, including bandwidth pricing, contact our Sales Team.

## Who Should Use CDN? What Kind of Content Is It Best Suited For?

Any company or individual that wants to make content available on the Internet should consider CDN, particularly those wanting to deliver content that requires large transfer rates, such as video. This includes a wide variety of industries, as caching, streaming, and downloading services are a regular part of social networking, entertainment, media, gaming, software, broadcast, e-commerce, and e-banking websites alike. In the past CDNs were so expensive that only large companies could use them. IBM Bluemix’s CDN brings the expense of operating a CDN down to a price more affordable by all types of companies and offers them a chance to use an enterprise-level product without the headache or high expense.
