---

copyright:
  years: 2019
lastupdated: "2019-06-17"

keywords: pricing, cost, faq, inbound message, minutes, call

subcollection: "voice-agent"


---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:deprecated: .deprecated}
{:external: target="_blank" .external}

# Pricing FAQs
{: #faq-pricing}

{{site.data.keyword.iva_full_notm}} is deprecated. As of 1 March 2021, you can't create new instances. Existing instances are supported until 31 December 2021. Any instance that still exists on that date will be deactivated. For more information, see the deprecation announcement [blog post](https://community.ibm.com/community/user/watsonapps/blogs/mitch-mason1/2021/02/08/announcing-voice-agent-with-watson-deprecation){: external}. You can use {{site.data.keyword.conversationfull}} integrations to enable voice and SMS interaction with your cognitive assistant. See the migration instructions for the {{site.data.keyword.conversationshort}} [phone integration](/docs/assistant?topic=assistant-deploy-phone#deploy-phone-migrate-from-va){: external} and [SMS with Twilio integration](/docs/assistant?topic=assistant-deploy-sms#deploy-sms-migrate-from-va){: external}.
{: deprecated}

## What is the price for using the {{site.data.keyword.iva_short}} standard service?
{: #faq-pricing-zero}
{: faq}

 For more information, see the [pricing page](https://cloud.ibm.com/catalog/voice-agent-with-watson){: external}.

## What does "pricing per minute" mean?
{: #faq-pricing-one}
{: faq}

The price is based on the amount (number of minutes) of audio that you send to the service. The price does not depend on how long the service takes to process the audio.


## Do you calculate to the nearest minute for every call to the API?
{: #faq-pricing-two}
{: faq}

'{{site.data.keyword.IBM_notm}} does not calculate the length of the audio for every API call that the service receives to the nearest minute. Instead, {{site.data.keyword.IBM_notm}} aggregates usage for the month and then calculates to the nearest minute at the end of the month. The duration of each call is rounded up to the nearest second. For example, if you make the first call for 3.1 sec and the second call for 25.9 sec, {{site.data.keyword.IBM_notm}} calculates the first call for 4 sec and the second call for 26 sec. Then, the duration of the total audio is calculated to one minute.'


## How is concurrent connection calculated and where is it applied?
{: #faq-pricing-three}
{: faq}

The concurrent connection is applicable to voice call only(Not SMS). Concurrent connection is calculated as the number of connections to any phone numbers defined in the service instance simultaneously. Actual daily maximum number of concurrent connections that are used is billed, prorated based on the monthly charge.

## What's the definition of maximum concurrent connection and how to change it?

{: #faq-pricing-four}
{: faq}

The maximum concurrent connection is the maximum number of connections that are allowed at any time, and it is the maximum number of connections that are billed. Maximum concurrent connections can be defined and changed in the [dashboard](https://cloud.ibm.com/docs/voice-agent?topic=voice-agent-edit_concurrency). The max concurrent capacity on a standard plan is 50 connections, and if you need more you can open a support ticket.

## How are inbound and outbound SMS/MMS messages billed?

{: #faq-pricing-five}
{: faq}

Inbound messages are not billed until a response is sent to the user. A session is created when an outbound message is sent to the user through Voice Gateway or as a response to an inbound message. Both the outbound and the inbound messages that are responded to are billed, if applicable.
Both the outbound and inbound messages are billed until the session times out. After the session times out, conversation context is discarded. The default session timeout is 3600 sec, and users can set up the duration of session timeout on the dashboard.
