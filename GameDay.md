## Building a gas station chatbot with AWS Lex, Lambda and Here services:

In this tutorial, we will deploy a small chatbot with AWS Lex and Here servies to help users find the gas stations near by a specified location. We will explore the combination of AWS services, Here API services and how they can be stitched together to create a powerful, scalable and secure application. To complete this tutorial, you will need: An AWS Account, basic knowledge of the AWS UI, account with developer.here.com ,and some basic understanding of node/Javascript.

# Step 1: Deploy Lex bot

Login to your AWS console, find Amazon Lex and click on it. Now, click on the create button to get started and then on the next screen, click Custom Bot, fill in the details as shown in the screenshot below.

![alt text](screenshots/step1.png "Step 1: Deploy Lex bot")

Once you fill in the all the required details click on *Create*
button to navigate to the next screen. 

![alt text](screenshots/step2.png "Create Intent")

On the next screen you will find Create Intent. An Intent is a objective or action the user wants to achieve. Think of an intent as the specific reason a user would want to send a message to your bot. Lets create an intent and call it gasStationNearBy. 

![alt text](screenshots/step3.png "Create Intent")

Once we’ve done that, we’re greeted with another screen with a whole bunch of input options. Lets focus on Slots first.

![alt text](screenshots/step4.png "Slots")

Slots are the variables of Lex. If someone was ordering a pizza, the Slots to include would be things like {SIZE}, {PIZZA_TYPE} and {DELIVERY_ADDRESS}. For our chatbot, we will have one slot. {gpsCodes}. There is a lot to discuss about slots and different slot types. Essentailly there are two types of slot available custom slots and builtin slots. For our chatbot we will be creating the custom slot. <a href="https://docs.aws.amazon.com/lex/latest/dg/howitworks-builtins-slots.html">So, I encourage you to see more information about slots on the amazon amazon docs</a>.

To create a custom slot, go ahead added new slot type from the left hand side menu, you will find a dialog box which will have create slot type(As shown in the screenshot below)

![alt text](screenshots/step5.png "Creating Custom Slots")

Once you click on the *create slot type* you will be greeted with a bunch of options to fill in. You can follow below screenshot to fill and go head and click on the *Add slot to intent*

![alt text](screenshots/step6.png "Creating Custom Slots")

Once the slot successfully saved, you can find the *gpsCodes* slot under the custom slot as shown in the below screenshot.

![alt text](screenshots/step7.png "selecting the custom slot to the intent")

Now that we have added the out custom slot, let us go ahead and setup the slot for our intent. As you can see in the following screenshot, we have to give a name to our custom slot, from the slot type dropdown please select gpsCodes under the *Custom slot types* and then give a prompt like so _which gps coordinates?_ Click on the add button under the settings to apply the slot to the current intent. Finally, click on the *Save Intent* button located on bottom of the page.

![alt text](screenshots/step8.png "applying the slot to the intent")

We need to add in variations of that utterance you can think of,but keep it relatively short to 2–3 different variations. Lets add the following utterances

* gas stations near {gpsCodes}
* petrol stations near {gpsCodes}
* fuel stations near {gpsCodes}

![alt text](screenshots/step9.png "Adding uttetances")

Notice for Fulfillment, you have the option to either send the intent to a lambda function or return parameters to client. For now, lets click Return Parameters to Client and click save. We’re going to check on our bot before moving over to Amazon Lambda and creating the business logic of our chatbot. Scroll down and save your intent.

![alt text](screenshots/step10.png "Adding Fulfillment")

And now for a bit of fun! On the top right of the dashboard, click Build. This will initialize your chatbot and allow you to begin testing it. A chat widget should pop up on the right side of the screen. Try it out!

![alt text](screenshots/step11.png "Building and testing the bot")