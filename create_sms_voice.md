---

copyright:
  years: 2019
lastupdated: "2019-06-24"
subcollection: "voice-agent"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Creating an SMS-enabled voice agent
{: #sms_config_instance}

After you have created your {{site.data.keyword.iva_full}} service, you can create individual voice agents with SMS functionality, or just voice agents with only SMS capabilities, from the _Manage_ dashboard.
{: shortdesc}


1. Go to the _Voice agents_ tab on the _Manage_ dashboard, and click **Create a Voice Agent**.

1. For **Agent Type**, select _Voice + SMS_.

1. Follow steps 3 through 6 in [creating a voice agent](https://test.cloud.ibm.com/docs/services/voice-agent?topic=voice-agent-config_instance).

1. Check **Initiate conversation from inbound messages** to allows users to begin an SMS session with your SMS agent. 

1. Check **Notify on session timeout** to have your SMS agent send an SMS message to the user, alerting them that the agent has not received a response in some time and will now timeout. 

    - See [Advanced Options](/docs/services/voice-agent?topic=voice-agent-sms_config_instance#sms_advanced) for more information on the **Advanced Options** available for your SMS agent, such as setting a custom time for the session to timeout.

1. Follow steps 4 through 7 in [creating an SMS agent](https://test.cloud.ibm.com/docs/services/voice-agent?topic=voice-agent-config_instance).

To enable SMS messaging between customers and a voice agent during a voice call, the SMS number must match the voice number.
{: tip}

Before you create an SMS agent or add SMS functionality to your voice agent, you **must** have the proper credentials setup and generate an API key to program to your SMS number. See [Generating API Key and Setting Credentials](/docs/services/voice-agent?topic=voice-agent-connect-sms#sms_access).

You **must** also configure your SIP trunk for SMS functionality. See your provider's instructions, for example, Twilio. If you do not have a Twilio phone number, see [Creating a Twilio SIP trunk](/docs/services/voice-agent?topic=voice-agent-connect#twilio-setup).

Once you have a Twilio number, you will need to configure it for SMS functionality. See [Configuring Twilio for SMS](/docs/services/voice-agent?topic=voice-agent-connect-sms#twilio-setup).

If you have trouble creating credentials, contact your service instance administrator to grant you *Manager* or *Writer* access.
{: tip}

## Advanced Options for SMS Agents
{: #sms_advanced}

Click **Show Advanced** after the **Phone Number** field.

1. Set an optional **Conversation read timeout** value. This is the time in seconds that the SMS Gateway waits for a response from Watson Assistant. If the time is exceeded, SMS Gateway reattempts to contact Watson Assistant. If the service still cannot be reached, the SMS/MMS message fails. Set to 30 seconds by default.

1. Set an optional **Session Timeout**. This is the time in seconds after which the session expires if SMS Gateway does not receive a response from the user.

1. Set an **Conversation failure reply message**. This is the default response message which is sent if Watson Assistant cannot be reached. By default, it is set to `We're sorry, but we can't respond to your message.`. 

### Configuring the SMS Agent for Outbound messaging
{: #sms_outbound}

You can configure your {{site.data.keyword.iva_full}} to receive inbound voice calls and respond with SMS outbound messages, depending on the voice command received by the user. To configure, add a node and intent in your {{site.data.keyword.conversationshort}} service.

* _**NOTE:**_ For an agent to have both Voice and SMS integration, such as receiving Voice input and sending back an SMS outbound message for a reply, you **must** use a one of your **voice** numbers for the **SMS** agent.

1. Create a **Voice + SMS** agent. Follow the instructions for [Creating a Voice Agent](/docs/services/voice-agent?topic=voice-agent-config_instance), or switch your **Agent Type** to **Voice + SMS**. 

1. In your {{site.data.keyword.Bluemix_notm}} dashboard, select the {{site.data.keyword.conversationshort}} instance that your voice agent uses.

1. From the _Getting started_ dashboard, click **Launch tool**.

1. Click **Getting Started** on the skill that you want to edit.

1. Click **Add intent** and enter a name for the intent, such as _Outbound_Text_.

  You can enter more detailed information, or return later to edit and refine the intent.

1. After you create your outbound messaging intent, select the _Dialog_ tab.

1. Click **Add node** and enter a name for the node, such as _SMS Outbound Text_.

1. In the _If the bot recognizes:_ section, type **SMS Outbound Text intent** to find the intent you made.

1. For the _Then respond with:_ section, click the **&vellip;** icon and select **Open JSON editor**. Copy and paste the following code snippet to replace the code in the field.

    ```json
        {
            "output": {
                "text": {
                "values": [
                    "Okay. I will send you a text message now."
                ],
                "selection_policy": "sequential"
                },
                "vgwActionSequence": [
                {
                    "command": "vgwActSendSMS",
                    "parameters": {
                    "message": "This is a test message from Watson Assistant"
                    }
                },
                {
                    "command": "vgwActPlayText"
                }
                ]
            }
        }
    ```
    {: codeblock}


1. Call your agent and trigger the node to receive a text message on the phone that you are calling from. 

To learn more about working in the {{site.data.keyword.conversationshort}} service, see [About {{site.data.keyword.conversationshort}}](/docs/services/assistant?topic=assistant-index#indext).

### Configuring the SMS Agent for Terminating the Session
{: #sms_terminate}

The {{site.data.keyword.iva_full}} SMS agent terminates a session based on the value for the session timeout, which is configurable and set to 30 seconds by default. 

You can also add a node to your {{site.data.keyword.conversationshort}} service to respond to an end session command from the user. 

1. In your {{site.data.keyword.Bluemix_notm}} dashboard, select the {{site.data.keyword.conversationshort}} instance that your voice agent uses.

1. From the _Getting started_ dashboard, click **Launch tool**.

1. Click **Getting Started** on the skill that you want to edit.

1. Click **Add intent** and enter a name for the intent, such as _Terminate SMS_. Alternatively, you can modify an existing intent that you already use for the voice agent, such as _End the call_.

  You can enter more detailed information, or return later to edit and refine the intent.

1. After you create your outbound messaging intent, select the _Dialog_ tab.

1. Click **Add node** and enter a name for the node, such as _Terminate SMS Text_.

1. In the _If the bot recognizes:_ section, type **Terminate SMS Text intent**, or the existing intent name you had, to find the intent you made.

1. For the _Then respond with:_ section, click the **&vellip;** icon and select **Open JSON editor**. Copy and paste the following code snippet to replace the code in the field.

    ```json
        {
            "output": {
                 "text": {
                    "values": [
                        "Thank you for using the service. Goodbye!"
                    ],
                    "selection_policy”: “sequential"
                },
                "smsAction": {
                    "command": "terminateSession"
                }
            }
        }
    ```
    {: codeblock}


1. Change the `values` field in the preceding code snippet to be your customized termination message to the user. 

After you create the voice agent, test your voice agent by calling or texting its phone number based on its type. You can view details about your interaction on the _Usage_ dashboard. See [Viewing Usage and Logs](/docs/services/voice-agent?topic=voice-agent-logging).  