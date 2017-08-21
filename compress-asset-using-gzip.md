---

copyright:
  years: 2017
lastupdated: "2017-06-29"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Compress an Asset Using Gzip

Gzip compression is a feature of the CDN that will optimize content delivery speed and allow for bandwidth savings due to smaller files being sent to capable browsers. How this works is that a request to the CDN is made, the requested file is delivered in a compressed format and the browser decompresses the file.  This feature is currently available only for Origin Pull configurations.

An asset can be compressed on an origin server before it is delivered to an edge server. The process through which requested content is compressed is outlined below.

1. A client requests content with a compression method defined in the Content-Encoding header.
2. If the asset is not already cached on the POP closest to the client, then the request is forwarded to an origin server.
3. If the origin server supports the specified compression method, it compresses the asset and sends it to an edge server.
4. An edge server serves the compressed asset to the client. After which, the compressed asset is cached on that edge server.
5. Subsequent requests to that POP are handled as detailed below.
**Note**: If an origin server does not support the requested compression method, it will serve the content in an uncompressed format to the edge server. At which point, the edge server can compress the asset, cache it, and then serve it to the client.

## How to Set Asset Compression:

1. Navigate to the **Cache Settings** page on the **HTTP Large Object** page in the MCC.
2. Select **Compression Enabled** option.
3. In the File Types list, make sure that only the desired content types are listed. For each content type that is not currently listed, append a comma and the content type (type/subtype).
4. Click **Update** to save your changes.
**Note**: Keep in mind that it may take up to an hour for your changes to take effect.

## How to Enable Gzip Compression

In order to enable Gzip support on the CDN the origin web server must include support for Gzip compression and needs to have the following http response headers:

Vary: Accept-Encoding
Content-Encoding: gzip
http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.3

Gzip support will work without the “Vary: Accept-Encoding” header however if a gzip or non-gzip compatible browser makes the initial cache the file will be forced served in the same way it was cached. Meaning that if a Gzip capable browser makes the initial request the non-capable browsers will also be forced to receive compressed content thus breaking the content. The “Vary: Accept-Encoding”  allows for the CDN to cache two copies of the file so that way a compressed and non-compressed copy will be available allowing for all browsers to access the content.  For more information on this refer to the rfc below:

By default neither of these headers may exist on the web server so you may need to modify your web server configuration accordingly.
To enable Gzip compression support on the origin web server these guides will help.

- [Compression for Apache 2.2](http://httpd.apache.org/docs/2.2/mod/mod_deflate.html)
- [Compression for Apache 2.0](http://httpd.apache.org/docs/2.0/mod/mod_deflate.html)
- [Compression for IIS 7](http://technet.microsoft.com/en-us/library/cc771003%28WS.10%29.aspx)
- [Compression for IIS 6](http://www.microsoft.com/technet/prodtechnol/WindowsServer2003/Library/IIS/92f627a8-4ec3-480c-b0be-59a561091597.mspx?mfr=true)
- [Compression for lighttpd](http://redmine.lighttpd.net/wiki/1/Docs:ModCompress)
- [Compression for nginx](http://wiki.nginx.org/NginxHttpGzipModule)

To manually add headers such as ``Vary: Accept-Encoding``  to the http response of the origin web server these guides will help as well.

- [HTTP headers Apache 2.2](http://httpd.apache.org/docs/2.2/mod/mod_headers.html)
- [HTTP headers  Apache 2.0](http://httpd.apache.org/docs/2.0/mod/mod_headers.html)
- [HTTP headers  IIS 7](http://technet.microsoft.com/en-us/library/cc753133%28WS.10%29.aspx)
- [HTTP headers  IIS 6](http://technet.microsoft.com/en-us/library/cc732442.aspx)
- [HTTP headers lighttpd](http://redmine.lighttpd.net/projects/lighttpd/wiki/Docs:ModSetEnv)
- [HTTP headers  nginx](http://wiki.nginx.org/NginxHttpHeadersModule)

**Note**: For IIS servers you may need to add the HcNoCompressionForProxies metabase key to the web server’s configuration as IIS by default will block requests containing the Via header which is standard in Squid proxy caching requests ( the CDN uses this for Origin Pull). For more information on this refer to [this article on #12](http://blogs.msdn.com/mike/archive/2007/12/06/troubleshooting-http-compression-in-iis6.aspx),
