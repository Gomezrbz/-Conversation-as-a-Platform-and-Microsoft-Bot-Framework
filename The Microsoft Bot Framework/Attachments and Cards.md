# Media Attachments
A message can certainly contain text strings, and of course various types of input actions, such as buttons, however, in the Microsoft Bot Framework a message exchanged between a user and a bot can contain images, videos, audio content, and even actual files, via the Attachments property.

The Attachments property of a message contains an array of Attachment objects that represent the media attachments and rich cards to display within a message, and writing this code would look very familiar to anyone who's worked with email or other messaging systems.

There are three (3) types of attachments that can be sent (although attachment support varies by channel) but the supported attachment types are media and files, cards, and hero cards.

- Media and Files: Send files such as images, audio and video

- Cards: Send a rich set of visual cards via JSON payload

- Hero Cards, See send a rich card containing a single large image, one or more buttons, and text.
### C#
In C#, adding an image as an attachment to a message requires an accessible location (URL), content type, and a display name:
``` 
replyMessage.Attachments.Add(new Attachment()
{
    ContentUrl = "https://www.traininglabs.io/bot-images/botimage.png",
    ContentType = "image/png",
    Name = "botimage.png"      
});
``` 

### Node.js

And, of course, in Node.js, almost the same code:
``` 
var attachment = msg.attachments[0];
session.send({            
    attachments: [
    {
        contentUrl: "https://www.traininglabs.io/bot-images/botimage.png",
        contentType: "image/png",
        name: "botimage.png"
    }]
});
``` 
To extend the concept of attachments, the Microsoft Bot Framework goes beyond simple image and file based content, and uses the powerful and flexible concept of cards.

## Cards Overview

In the Microsoft Bot Framework, a card comprises a title, description, link, and images. Some channels, such as Skype and Facebook, support sending these rich graphical cards to users, which can include interactive buttons. In the Microsoft Bot Framework these cards are, appropriately enough, referred to as rich cards. A message can contain multiple rich cards, displayed in either list format or carousel format.

The Bot Framework currently supports eight (8) types of rich cards:

- Adaptive: A customizable card that can contain any combination of text, speech, images, buttons, and input fields. See per-channel support.
- Animation: A card that can play animated GIFs or short videos.
- Audio: A card that can play an audio file.
- Hero: A card that typically contains a single large image, one or more buttons, and text.
- Thumbnail: A card that typically contains a single thumbnail image, one or more buttons, and text.
- Receipt: A card that enables a bot to provide a receipt to the user. It typically contains the list of items to include on the receipt, tax and total information, and other text.
- Sign in: A card that enables a bot to request that a user sign-in. It typically contains text and one or more buttons that the user can click to initiate the sign-in process.
- Video: A card that can play videos.
bulb icon To determine the type of rich cards that a channel supports and see how the channel renders rich cards, you can use the Channel Inspector covered in the previous lesson, or consult the channel's documentation for information about limitations on the contents of cards.

As you may recall, the Bot Connector handles communication between a bot and a third-party service (channel) and is also responsible for managing and normalizing messages. This means the Bot Connector will render these cards using schema native to the channel, providing supporting cross-platform communication.

If the channel does not support cards, such as SMS, the Bot Framework will do its best to render a reasonable experience to users.

Creation of a rich card is as simple as spinning up a card type, and adding it to the Attachments array, just like any other message attachment.

### C#

Creating a Thumbnail Card in C#:
``` 
ThumbnailCard plCard = new ThumbnailCard()
{
    Title = $"I'm a thumbnail card about {cardContent.Key}",
    Subtitle = $"{cardContent.Key} Wikipedia Page",
    Images = cardImages,
    Buttons = cardButtons
};

Attachment plAttachment = plCard.ToAttachment();
replyToConversation.Attachments.Add(plAttachment)
``` 
Or a Receipt Card might look like this:
``` 
ReceiptCard plCard = new ReceiptCard()
{
    Title = "I'm a receipt card, isn't this bacon expensive?",
    Buttons = cardButtons,
    Items = receiptList,
    Total = "112.77",
    Tax = "27.52"
};

Attachment plAttachment = plCard.ToAttachment();
replyToConversation.Attachments.Add(plAttachment);
``` 
And finally, a Sign In Card is even easier:
``` 
SigninCard plCard = new SigninCard(title: "You need to authorize me", button: plButton);

Attachment plAttachment = plCard.ToAttachment();
replyToConversation.Attachments.Add(plAttachment);
``` 
Up until now, you've been working with activities and messages as a single entity, and have a good feel for creating and formatting messages. You've also got a pretty good handle on using standard and rich card attachments to create more engaging messages. However, in the real world, bot experiences are part of a full conversation, with potentially complex relationships between messages, replies, and actions.

To work with full conversations, especially “guided” conversations, the Microsoft Bot Framework uses the notion of dialogs and forms.