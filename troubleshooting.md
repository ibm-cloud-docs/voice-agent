---

copyright:
  years: 2017, 2018
lastupdated: "2018-06-14"

keywords: troubleshooting, support, faq, help

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

# Troubleshooting and support
{: #troubleshooting}

{{site.data.keyword.iva_full_notm}} is deprecated. As of 1 March 2021, you can't create new instances. Existing instances are supported until 31 December 2021. Any instance that still exists on that date will be deactivated. For more information, see the deprecation announcement [blog post](https://community.ibm.com/community/user/watsonapps/blogs/mitch-mason1/2021/02/08/announcing-voice-agent-with-watson-deprecation){: external}. You can use {{site.data.keyword.conversationfull}} integrations to enable voice and SMS interaction with your cognitive assistant. See the migration instructions for the {{site.data.keyword.conversationshort}} [phone integration](/docs/assistant?topic=assistant-deploy-phone#deploy-phone-migrate-from-va){: external} and [SMS with Twilio integration](/docs/assistant?topic=assistant-deploy-sms#deploy-sms-migrate-from-va){: external}.
{: deprecated}

Having trouble with {{site.data.keyword.iva_full}}? Review the troubleshooting tips for common problems, and reach out to the community with any questions.
{: shortdesc}

## How to troubleshoot {{site.data.keyword.iva_short}}
{: #how-to}

To troubleshoot issues with your agents, you can use logging, usage, and event-forwarding to find records of errors and failures. These records can help you diagnose and resolve problems with your agents. If you are having trouble with {{site.data.keyword.iva_short}}, try the following steps.

1. When a call fails, the final {{site.data.keyword.conversationshort}} turn might explain the failure.

1. Usage logs show you any errors that occurred during a particular call. See [Viewing usage and call logs](/docs/voice-agent?topic=voice-agent-logging).

1. Check your service provider logs for signaling errors. For example, Twilio provides logs for each SIP trunk it hosts.

1. By [enabling event forwarding for agents](/docs/voice-agent?topic=voice-agent-event_forwarding), you can configure your agent to forward Call Detail Records (CDRs) to a Cloudant database and then determine why a call failed. Other events, such as {{site.data.keyword.conversationshort}} Turn Events can provide details about every conversation turn within a call.

**Important:** The CDR, transcription, and turn events include information from your users that might potentially contain Protected Health Information (PHI), personally identifiable information (PII), or PCI Data Security Standard (PCI DSS) data. To prevent exposure of personal information, you must ensure that your {{site.data.keyword.cloudant_short_notm}} instance properly protects the confidential information that your users share in or during conversation.


## Getting help
{: #help}

If you need help, join our developer community by posting your questions or comments to any of the following places, which are all actively monitored.

* Post on the [dwAnswers forum ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/voice-agent/) with the `voice-agent` tag
* Post on [StackOverflow ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://stackoverflow.com/questions/tagged/voice-agent){: new_window} with the `voice-agent` tag
* Find us on Slack in the [IBM Cloud Technology ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://slack-invite-ibm-cloud-tech.mybluemix.net/) team under the `#ibmvoicegateway` channel

**Remember**: Before you post any logs or records of calls, remove all personal information that your callers and users shared during conversation.

## Troubleshooting tips
{: #troubleshooting-tips}

### Why don't I get a response on the phone when I call my agent?

Your call likely didn't connect to the services. This problem occurs when the {{site.data.keyword.iva_short}} service instance isn't set up correctly. Check the following agent settings:

* Verify that the phone number on the agent _Manage_ dashboard is the same phone number from your SIP trunking provider, such as NetFoundry or Twilio.

   **Note:** You must include the country and area code when you specify the phone number on the agent _Manage_ dashboard. For example, `18884253968`.

* Verify that the Watson service credentials, URLs, and the {{site.data.keyword.conversationshort}} workspace ID are all valid.
* Verify that the dialog in your {{site.data.keyword.conversationshort}} skill was created correctly.
  * You can import the [sample conversation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/WASdev/sample.voice.gateway/blob/master/conversation/voice-gateway-conversation-en.json) from GitHub for a pre-built skill. See [Step 3 in *Getting started tutorial*](/docs/voice-agent?topic=voice-agent-getting-started#step3) for details about saving the sample conversation as a JSON file and then importing the file as a skill in the {{site.data.keyword.conversationshort}} tool.
  * If you created your own {{site.data.keyword.conversationshort}} dialog, verify that the dialog contains a node with the `conversation_start` condition and a node with a default response. For detailed instructions, see [Building a dialog](/docs/assistant?topic=assistant-getting-started#getting-started-build-dialog) in the {{site.data.keyword.conversationshort}} documentation.
* See whether your phone call is listed on the agent _Usage_ dashboard. If you see an item for your phone call, then your agent connected to the Watson service.

### Why can't I specify a phone number when I create an agent?

See whether the phone number you specified is used by an existing agent. You can have only one agent for a phone number. You can provision another phone number from your SIP trunking provider and use it to create another agent. Or [delete the existing agent on the _Manage_ dashboard](/docs/voice-agent?topic=voice-agent-managing#delete_va) to free up the phone number and then create a new agent.

### Why are my calls failing frequently?

Voice agents can have problems when calls fail because a Service Orchestration Engine (SOE) initiates a long transaction, and it does not respond to your voice agent in a timely manner. If a transaction exceeds the default {{site.data.keyword.conversationshort}} timeout, the call fails. To avoid call failures, the SOE can modify the default {{site.data.keyword.conversationshort}} timeout by using the `vgwConversationResponseTimeout` state variable. See [Variables set in the {{site.data.keyword.conversationshort}} dialog](https://www.ibm.com/support/knowledgecenter/SS4U29/api.html#variables-conv).

### Why do I receive `vgwNetworkWarningMessage` messages in the Watson Assistant dialog?

The  `vgwNetworkWarningMessage` message indicates that a network error condition occurred. For more information, see [Monitoring RTP audio streams by using RTCP](https://www.ibm.com/support/knowledgecenter/SS4U29/rtcpnetworkmonitor.html). To discontinue conversational turns when a network error condition occurs, disable the `Notify Watson Assistant on network events` option on the Edit Agent page. Under the `Description` field, click `Show Advanced` and clear the `Notify Watson Assistant on network events` option.

### Various Limitations

* You can create new Watson service instances directly from the _Create an Agent_ dashboard for either the **Dallas** or **Washington DC** regions. To connect your agent to Watson services in other regions, create your Watson services before you create a agent on the _Manage_ dashboard.

* Only connections to the public switched telephone network (PSTN) are supported.

* All agent configurations must be specified in the {{site.data.keyword.conversationshort}} service that uses the API.
