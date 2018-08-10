# Dialog Concepts
In the Microsoft Bot Framework, dialogs enable developers to “model” conversations and manage conversation flow. Although bots send and receive messages, a bot actually communicates with a user via a full conversation. Based on this idea, every conversation is organized into a series of dialogs.

Using the Bot Builder SDK, bot dialog steps can follow a “waterfall model”, as well as integrate a series of prompts, wherein a bot will start, stop, and switch between various dialogs in response to user messages. Understanding how dialogs work is key to successfully designing and creating great bots.

:bulb: The concept of a “waterfall model” generally means a relatively linear sequential design or flow.

In more familiar terms, dialogs are a way of wrapping an entire “experience” into an easily managed interaction based on a “chained” and “conversational” paradigm.

- Send information to a user
- Prompt a user for more information or confirmation
- Provide conditional logic
- Provide “as you need it” content
- Can contain or forward to other dialogs.
- Spinning up a dialog is as easy as working with messages and attachments. Here's an example of creating a dialog using Node.js:
``` 
bot.dialog('greetings', [
    function (session) {
        builder.Prompts.text(session, 'Hi! What is your name?');
    },
    function (session, results) {
        session.endDialog(`Hello ${results.response}!`);
    }
]);
``` 
Or a more complex “confirmation” example using C#:
``` 
PromptDialog.Confirm(
                context,
                AfterResetAsync,
                "Are you sure you want to reset the count?",
                "Didn't get that!",
                promptStyle: PromptStyle.None);
``` 
In fact, using the Bot Builder .NET SDK, extremely complex scenarios, including dialog chaining, can be accomplished with just a few lines of code:
``` 
new Regex("^chicken"),
            (context, text) =>
                Chain
                .Return("why did the chicken cross the road?")
                .PostToUser()
                .WaitToBot()
                .Select(ignoreUser => "to get to the other side")
``` 
As you can tell, dialogs are powerful and flexible, but handling a guided conversation, such as ordering a sandwich, or making an airline reservation, could require quite a bit effort, as there are potentially a large number of possibilities for what could happen next. To work with guided conversations, the Bot Builder SDK introduces the concept of forms.

## Form Concepts
Although Microsoft Bot Framework dialogs are the basic building block of a bot conversation, it’s difficult to create a “guided” conversation, with dialogs. By leveraging the concept of forms, users can be guided through the relevant steps of a full conversation—similar to the process of filling out a traditional form—and your bot logic can easily provide help and guidance along the way.

Creating bot conversation forms is driven by your choice of development language. For .NET developers, the Bot Builder SDK enables forms via strongly typed and attributed C# classes. For Node.js scenarios, form definition occurs via a well-formatted JSON schema.

For example, in C#, a form option could look like this:
``` 
public enum SauceOptions
{
    ChipotleSouthwest, HoneyMustard, LightMayonnaise, RegularMayonnaise,
    Mustard, Oil, Pepper, Ranch, SweetOnion, Vinegar
};
``` 
And for Node.js, this same form option could be similar to the following:
``` 
"Sauces": {
    "type": [
    "array",
    "null"
    ],
        "items": {
        "type": "string",
        "enum": [
            "ChipotleSouthwest",
            "HoneyMustard",
            "LightMayonnaise",
            "RegularMayonnaise",
            "Mustard",
            "Oil",
            "Pepper",
            "Ranch",
            "SweetOnion",
            "Vinegar"
    		]
    }
}
``` 
Although this process is pretty straightforward, full implementation of a form-based guided experience would require a combination of prompts, choices, and options. To combine these types of form elements into a single, cohesive flow, the Bot Builder SDK uses the notion of FormFlow.