---

copyright:
  years: 2017
lastupdated: "2017-06-28"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Add Origin Pull Mapping to a CDN Account

Origin Pull mapping allows the content requested by a user to be pulled from your origin server rather than the CDN FTP server. Origin Pull mapping enables you to manage content in a single location on your server, rather than managing content on the CDN FTP server, as well. Content is cached from your server and when requested, is produced for the user. Follow the steps below to add Origin Pull mapping to a CDN Account.

## Add Mapping

1. Access the CDN screen. Refer to [Access the CDN Screen](access-cdn-screen.html).
2. Click the **Account ID** for the desired CDN Account to access the account.
3. Click the **Add Mapping** link.
4. Complete each field in the pop-up box to set up mapping for the account. Refer to the table below for more information:
<table>
<tbody>
<tr>
<th>Field</th><th>Entry</th></tr>
<tr><td>Media Type</td><td>Type of media to be produced when the content is requested. Select HTTP.</td></tr>
<tr><td>Origin Base URL</td><td>The domain that hosts the media being requested. This is generally a specific URL, but may also be the CDN FTP space.</td></tr>
<tr><td>CNAME</td><td>The customized URL that will appear when content is requested from the CDN Account. <br/>If a CNAME is not designated, the default CDN URL will be displayed at the bottom of the pop-up box.</td></tr>
</tbody>
</table>

5. Click the **Save** button to save the mapping. Click **Cancel** to cancel the action.

## What Happens Next

After adding origin pull mapping to the CDN Account, the cached content will be stored on the [Customer Portal](https://control.softlayer.com/) and produced for the user when it is requested. It may be updated or removed at any time.
