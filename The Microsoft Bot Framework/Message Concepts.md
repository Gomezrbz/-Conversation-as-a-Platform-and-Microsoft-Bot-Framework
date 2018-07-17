# Message Overview

In the Microsoft Bot Framework, bots send message activities, or simply messages, to communicate information to users, and likewise, also receive messages from users.


## The message activity

**A message activity is used to communicate information to and from a user**. Some messages may simply consist of plain text, while others may contain richer content such as:

- Text to be spoken
- Suggested actions
- Media attachments
- Rich cards
- Channel-specific data 

Sending a bot message follows the same process, but happens a bit differently, depending on your development language. For example, sending a basic message using Node.js might look like this:
```
var customMessage = new builder.Message(session)
    .text("The Microsoft Bot Framework is awesome!")
    .textFormat("plain")
    .textLocale("en-us");
session.send(customMessage);
```
However, sending a message via C# would look more like this:
```
IMessageActivity message =  Activity.CreateMessageActivity();
message.Text = "The Microsoft Bot Framework is awesome!"; 
message.TextFormat = "plain";
message.Locale = "en-us";
await connector.Conversations.SendToConversationAsync((Activity)message);
```
At the most basic level, messages may simply consist of plain text, however the Microsoft Bot Framework supports the creation of messages containing enhanced content such as text to be spoken, suggested actions, media attachments, rich cards, and even channel-specific data.

However, before we take dig into rich content, let's take a look at the most basic and common scenario: creating and formatting messages.

## Creating and Formatting Messages

Text formatting can enhance your text messages visually. Besides plain text, your bot can send text messages using markdown or xml formatting to channels that support them. Most developers are familiar with xml formatting, as its been a standard for over 20 years, however markdown has quickly become the formatting standard for just about everything. In fact, this course was originally created in markdown before being converted to HTML.

If you're not familiar with markdown, markdown is a lightweight markup language with plain text formatting syntax. Markdown is specifically designed to be easily converted HTML and many other formats and is often used to format readme files, writing messages in online discussion forums, and to create rich text using a plain text editor.

When creating conversation bot messages, markdown is ideal, as it provides simple syntax for highlighting and accentuating content with very little effort.

The following are some of the most commonly used text formatting in markdown.

bold: **text** (text)
italic: *text* (text)
strikethrough: ~~text~~ (text)
preformatted text:  (code block)

Creating messages using plain and formatted text is a breeze, however what if a user wants (or needs) to interact with your bot verbally? For this we need to take a look at text to be spoken, or spoken text.

## Spoken Text

When creating bots for a speech-enabled channels, such as Cortana, you can easily construct messages that specify the text to be spoken by your bot. This feature can be enhanced, as well, by providing an “input hint” which will attempt to influence the state of the client's microphone, or indicate whether your bot is accepting, expecting, or ignoring user input.

In the Microsoft Bot Framework, there are multiple ways to specify the text to be spoken by your bot on a speech-enabled channel. For example, you can either use the SayAsync method, or specify the Speak property of the message to specify the text to be spoken by your bot.

In C#, creating a message activity and setting the Speak property might look like this:
```
Activity reply = activity.CreateReply(); 
reply.Speak = "This is the text that will be spoken.";
reply.InputHint = InputHints.AcceptingInput;
await connector.Conversations.ReplyToActivityAsync(reply);
```
In Node.js, it's almost the same code:
```
var msg = new builder.Message(session)
    .speak('This is the text that will be spoken.')
    .inputHint(builder.InputHint.acceptingInput);
session.send(msg).endDialog();
```
With a good bot conversation flow, input hints and spoken text can go a long way to providing a great user experience, however the reality is: your bot will always know more about what actions can be taken than a user will. Luckily, the Microsoft Bot Framework provides the concept of suggested actions.

## Suggested Actions

If you imagine a scenario where a bot is attempting to determine, for example, a paint color for an order, it would be pretty tough for a user to figure out all possible color choices. In these instances, suggested actions enable your bot to present pre-defined choices (based on what a bot already knows) as buttons, that the user can tap,

To clarify: suggested actions enhance the user experience by enabling the user to answer a question or make a selection with a simple tap of a button, rather than having to type a response with a keyboard.

bulb iconUnlike buttons that appear within rich cards (which remain visible and accessible to the user even after being tapped), buttons that appear within the suggested actions pane will disappear after the user makes a selection. This prevents the user from tapping stale buttons within a conversation and simplifies bot development (since you will not need to account for that scenario).

Providing suggested actions is, again, a simple process. In C#, your code might look like this:
```
var reply = activity.CreateReply("Thank you for expressing interest in our premium exterior paint colors! What color of paint would you like?");
reply.Type = ActivityTypes.Message;
reply.TextFormat = TextFormatTypes.Plain;

reply.SuggestedActions = new SuggestedActions()
{
    Actions = new List<CardAction>()
    {
        new CardAction(){ Title = "Mauve", Type=ActionTypes.ImBack, Value="Mauve" },
        new CardAction(){ Title = "Cornflower Blue", Type=ActionTypes.ImBack, Value="CornflowerBlue" },
        new CardAction(){ Title = "Aztec Pink", Type=ActionTypes.ImBack, Value="AztecPink" }
    }
};
```
If you're working with Node.js, it's just as easy:
```
var msg = new builder.Message(session)
	.text("Thank you for expressing interest in our premium exterior paint colors! What color of paint would you like?")
	.suggestedActions(
		builder.SuggestedActions.create(
				session, [
					builder.CardAction.imBack(session, "productId=1&color=mauve", "Mauve"),
					builder.CardAction.imBack(session, "productId=1&color=cornflowerblue", "Cornflower Blue"),
					builder.CardAction.imBack(session, "productId=1&color=aztecpink", "Aztec Pink")
				]
			));
session.send(msg);
```

bulb icon In the Microsoft Bot Framework, imBack method will post the value to the chat window of the channel you are using. If you do not want the value to appear in the chat windows after selection, you can use the postBack method instead, which will post the selection back to your bot, but will not display the selection in the chat window.

With a quick taste of what the Microsoft Bot Framework and Bot Builder SDK can provide, you might be ready to write some code of your own, however “hosting” a bot requires a little more knowledge. As with all software development, having a reliable test environment could make all the difference.

In bot development with the Microsoft Bot Framework, these tasks occur via the Bot Framework Emulator, which is provided as a separate component, and needs to be installed and configured.