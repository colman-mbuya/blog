---
title: "TIL: Google Access Transparency"
date: 2020-04-22
categories:
- til
- gcp
- g-suite
tags:
- til
- gcp
- logging
thumbnailImagePosition: left
thumbnailImage: images/transparency.jpg
---

[Google Access Transparency](https://cloud.google.com/logging/docs/audit/access-transparency-overview) is a service available in GCP and G-Suite that allows organisations to view logs pertaining to resource access by Google support staff. There are many reasons why Google might access your resources, for example in response to support requests, to investigate whether an issue seen elsewhere is present in your environment or to verify compliance with their terms and conditions. 

The service is only available to organisations that meet the following criteria:
- G-Suite Enterprise or Enteprise for Education is in [use](https://support.google.com/a/answer/9230979?hl=en) 
- The GCP organisation meets one of the [following criteria](https://cloud.google.com/logging/docs/audit/access-transparency-overview#requirements): 
    - Your Google Cloud organization has one of the following role-based Support packages: 
        - Enterprise Support 
        - Four or more Development roles 
        - Four or more Production roles 
        - A combination of four or more Development or Production roles 
    - Your Google Cloud organization has one of the following Support packages: 
        - Platinum Support 
        - Gold Support 

> Note: Development and production roles refer to the level of support subscription as described in the support page on the console 
![Dev and prod roles](/images/support_levels.png)

I don't have access to a GCP organisation or G-Suite subscription that meets these conditions, so I couldn't take a detailed look at how the service works. However, from reviewing the service documentation on [reading the logs](https://cloud.google.com/logging/docs/audit/reading-access-transparency-logs) for GCP, it looks like these logs could provide useful indicators of unauthorised access. For example, in GCP, whenever Google accesses your resources in response to a support ticket, they would include the `CUSTOMER_INITIATED_SUPPORT` justification reason code in the transparency log entry together with the support ticket number. These types of logs could be useful to monitor for case numbers that you aren't aware of. Other interesting justification reason codes, based on their descriptions, are `GOOGLE_INITIATED_REVIEW` and `GOOGLE_INITIATED_SERVICE`. 

![Justification Codes](/images/justification_codes.png)

The logs in GCP are available via the standard Logging service in the console. One shortcoming is the log entries don't seem [super detailed](https://cloud.google.com/logging/docs/audit/reading-access-transparency-logs#sample-log). For example, they seem to only include the project name and type of resource accessed but not the specific name of the resource e.g. kubernetes cluster name. Additionally, there are some exclusions on when access gets logged. Though some of these make sense, such as when complying to a legal request where Google are not allowed to tell you why. More details on exclusions can be found [here](https://cloud.google.com/logging/docs/audit/access-transparency-overview#excluded).

In G-Suite, the [logs and restrictions](https://support.google.com/a/answer/9230979?hl=en) are similar to the above.

Overall, if you can enable Access Transparency, it's probably a good idea for the following reasons:
- Monitoring of unauthorised support tickets
- As an indicator of potential compromise or issues on Google's side
- To comply with your own internal audit requirements