---

copyright:
  years: 2017
lastupdated: "2017-07-07"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# How do I Purge Content from the CDN?
Content that has been cached on an edge server can be purged at any time. A typical reason for why you would want to purge on-demand content is that you have a newer version of an asset.  In such a case, the old version of the asset will continue to be served out by our edge server until it either checks for a new version, the content expires, or it is purged.

**Important**: Purging is not the same thing as deleting content from the origin server. Purging an asset will not delete the source asset. It will simply remove the cached instance of that asset from all of our edge servers. If you would like to remove the original asset, then you will need to delete it from the origin server through your preferred FTP client.

## Automated Purging Through Content Expiration:
You can specify content expiration headers from your web server. This will automatically tell our edge servers how often to check for content freshness, and will automatically y purge content that is no longer needed. For example, setting the header on your web server to "cache-control: max-age=86400" would cause our edge server to check for a new version of an asset every 86400 seconds (i.e. on a daily basis). If the revalidation with the origin server indicates that the requested asset is outdated or no longer exists, then the cached version of that asset will be purged.

**Note**: If an edge server successfully revalidates a cached version of an asset, then the expiration time will automatically get updated. This means that the cached version of the asset will be assigned new Cache-Control and Expires headers based on the response returned from the origin server. If these headers have not been defined, then the asset will be assigned a default max-age of 7 days from the time it was successfully revalidated. Please refer to your web server\’s documentation for more information on how to configure these settings.

## Manually Purging Assets
Cached assets can be purged from our edge servers through the My Edge page, which can be found on the HTTP Large tab of the MCC. Keep in mind that you may purge assets individually, by folder, or recursively.

**Tip**: If you have assets that are updated frequently, then you should consider using a naming convention that assigns unique names to your new assets. This will ensure that future requests will go to the new assets without the need of manual y purging the old assets.

**Tip**: An alternative to changing your file naming convention for assets that are updated frequently is to use the Bulk Purge option. This option allows you to specify a list of assets that will be placed into the purge queue. If you keep a record of frequently purged assets, then you can copy and paste them into this option. Please keep in mind that there is a default limit of 50 concurrent purge requests at any given time.

**Note**: An asset only needs to be purged a single time per location. The asset will be purged regardless of the CNAME used to reach it; provided that those CNAME records point to the same location.

### To manually purge assets:

1. Navigate to the **My Edge** page, which can be found on the HTTP Large tab of the MCC.
2. Under the **Purge From Edge** section, select the location of the asset(s) that you would like to purge from the Purge URL option.
3. To the right of the **Purge URL** option, type the path to the folder containing the asset(s) that you would like to purge. Make sure that the path starts with a forward slash (/).
4. Perform one of the following and then click **Purge**:
   - To purge a specific asset: Append the name of the asset that you would like to purge to the relative path specified in step 3. If you would like to purge assets based on query strings, please refer to the Purging Query String Variations of a Cached Asset section below.
   - To purge a set of assets: Determine the naming convention and/or file type that will be used to identify the assets that will be purged. Append that pattern to the relative path specified in step 3 (for example `/2012/July*.ht*`).
   - To purge a folder’s content: Append a forward slash, an asterisk `(/*)`, a period, and another asterisk to the relative path specified in step 3 (for example `/2012/*.*`).
   - To recursively purge a folder\’s content: Make sure that the path points to the folder whose contents you would like to purge and that a forward slash and an asterisk `(/*)` follow the name of the desired folder.

**Important**: The Purge button applies to both the Purge URL and the Bulk Purge option.  However, the Bulk Purge option takes precedence over the Purge URL option. This means that the Purge URL option will be ignored when the Bulk Purge option contains a value.

**Important**: An asterisk ``(*)`` can either be used as a wildcard in a file name pattern or to recursively purge a folder\’s content. However, it cannot be used as a wildcard when specifying a directory. Additionally, you should keep in mind a recursive purge is always performed for purge requests that end with a forward slash followed by an asterisk `(/*)`. If you would like to purge a folder\’s content, append `/*.*` to the desired purge directory.

**Note**: Each purge request needs to be processed. Therefore, your request will be placed in a queue. The My Edge page provides a means to keep track of when a request was made and when it was completed.

## Bulk Purge:

1. Navigate to the **My Edge** page, which can be found on the **HTTP Large** tab of the MCC.
2. In the **Bulk Purge** option, type the **CDN** or **edge CNAME URL** that points to the asset that will be purged.
3. If you would like to purge another asset, press **ENTER** and then specify the desired **CDN** or **edge CNAME URL**. Repeat this step as needed.
4. Click **Purge**.

**Note**: Each CDN or edge CNAME URL specified in the Bulk Purge option must be placed on a separate line. This can be accomplished by using a carriage return to delimit each CDN or edge CNAME URL. Using any other type of character (such as a comma) as a delimiter may prevent the asset from being purged. 
