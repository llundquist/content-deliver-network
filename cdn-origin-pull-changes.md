---

copyright:
  years: 2017
lastupdated: "2017-07-12"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# CDN Origin Pull Changes 

## Origin Pull     

In most cases, the recent changes in the CDN platform do not require you to change your Origin Pull configuration and CNAMEs. After the update, you should only find three primary changes overall:     

 - New Account Names
 - Content Authentication Username and Password No Longer Supported
 - Windows Media Pull No longer Supported
        

### New Account Names     

The new CDN service does not allow nor require custom account names so we will be assigning new account names. This will only effect you if you generated your CDN links using the URL http.CDN.com// and did not use a CNAME.  If this is the case, you should start using a CNAME now and recode your links accordingly. The old URL will no longer work and your links will eventually fail.  Additionally usage of a CNAME simplifies your URLs and we do not charge for this service.     

### Content Authentication     

You will no longer have the ability to add HTTP content authentication credential handling. Most clients do not use this authentication so if you are unsure you will most likely not even be affected.     

### Windows Media     

Windows Media will no longer be supported for Origin Pull.
