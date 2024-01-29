# Setting Up Call Recording Notifications with SignalWire and Zapier

In this guide, we will walk you through the process of using SignalWire's call flow builder in conjunction with Zapier to automate the delivery of call recordings to your email address. This will help you stay up to date on your callers and ensure that you have access to your customers' messages anywhere.

## Getting Started

First, you will need to set up a Call Flow Builder flow to handle your incoming calls. Design the flow that suits your specific use case. For information on building with the Call Flow Builder, refer to [this link](https://developer.signalwire.com/guides/getting-started-without-code/#call-flow-builder).

For the purpose of this guide, I've created a simple voicemail catcher. If you want to follow along, here is my exact flow.

Once you have your call flow set up for your specific use case, the next step is to add a request node. This node will be responsible for sending a request to Zapier to handle your email notifications. Follow the instructions below to configure this node correctly:

### Request Node Settings

**URL:**
- Set the URL to your Zapier Webhook URL. Leave this field empty for now, and we'll create this URL in Zapier shortly.

**Method:**
- Choose "POST" as the method. This instructs the system to send data to Zapier using the POST request.

**Headers (JSON):**
- Leave this section empty. No additional headers are required for this integration.

**Body:**
- In the body section, include the following specific text. This text will be sent to Zapier as part of the request: 
```You received a call from %{call.from}. Voicemail:%{record_url}```

**Condition:**
- Set the condition to "200". This is the expected response code from the webhook, indicating a successful retrieval of data by Zapier.

*The final result should look like the image below (add image or diagram if available).*

## Finishing Up with Zapier

Now that we have completed our call flow with Call Flow Builder, we need to create our Zap. If you haven’t already, go to [zapier.com](https://zapier.com/) and create an account. Once done, click "Create a Zap" in your dashboard.

You should now see “Trigger,” press this and select “Webhooks by Zapier.” For the event, choose “Catch Raw Hook.” This should be the final result.

Press continue and copy the URL provided and paste it in the “URL” slot of your Call Flow Builder's request node. This is where it will send the POST request with all the data. Once you have the URL in the slot, deploy the script and give it a call! We will need to have the webhook tested for our next steps.

Once you’ve placed a call, you should see something similar to this:

Select this record as this is what we will be using to pull our call data. You should see the caller’s number and their voicemail URL within the “raw_body”. Now we will need to add another trigger. Press the “+” icon and add a “Formatter by Zapier”. For the event, choose “Text” and press continue. For transform, select “Extract Phone Number.”

After selecting “raw_body” as the input, the phone number format can be universal or whichever works best for your region of numbers that dial you. After all is done, it should look like this.

Now for the final step! Select the “+” icon to add another trigger for the last time. For this one, select “Email by Zapier” and for the event, select “Send Outbound Email”. From here, you will need to enter your email address, a subject with the formatted number by inserting the data from our number formatter, and finally insert the “raw_body” from our webhook. It should look like this after all is done.

You are now all set! Give it a test and see if you receive the email. Once everything is confirmed working, go ahead and press publish.

## More Zapier

Want to learn more about what you can do with Zapier and SignalWire? We have even more fantastic guides about exactly this. Explore additional guides:

- **Creating a Zap:** [Link to Guide](https://developer.signalwire.com/guides/how-to-integrate-signalwire-with-zapier)

- **Zapier Webhooks:** [Link to Guide](https://developer.signalwire.com/guides/use-webhooks-by-zapier-with-signalwires-apis)

## Conclusion

By following this guide, you can easily set up a system that automatically sends call recording notifications to your email address using SignalWire's call flow builder and Zapier. This helps you stay informed about your customers and their interactions with your business.
