# Overview of the Microsoft Bot Framework

The Microsoft Bot Framework is a powerful set of services, tools, and SDKs, providing a rich foundation or “framework” for developers to build and connect intelligent bots. By leveraging the Microsoft Bot Framework, developers can create, integrate, and manage a wide variety of bots and bot experiences that interact with users naturally.

## The Microsoft Bot Framework

More importantly, the Microsoft Bot Framework make it easy for developers to design and build bots that support a wide variety of user interactions. Developers can design freeform, loosely coupled conversations or create logic for more guided interactions—where a bot provides specific, well-known user choices or actions. Using the Bot Framework, conversations can display simple text strings or contain complex, “rich” cards containing text, images, video, animation—even buttons that perform actions. Combined with natural language interactions, users interact with your bots in a natural and expressive way.

Regardless of the tools, platform, and user audience, bot developers all face the same challenges: bots require basic I/O, bots need to have at least basic language and dialog skills, bots need to connect and interact with users in a language understood by the user, and bots need to be available in the services users need them.

To address these complexities, the Microsoft Bot Framework provides a comprehensive set of tools, services, and documentation for bot development—the Microsoft Bot Builder SDK.

## The Bot Builder SDK

The Microsoft Bot Framework provides everything a developer would need to build, connect, and manage intelligent bots, however understanding and managing these working parts would be a challenge, without development tools and documentation to harmonize these powerful services. This is where the Bot Builder SDK comes into the picture.

In a nutshell the Microsoft Bot Builder SDK provides:

- A powerful, easy-to-use framework that provides a familiar way for .NET and Node.js developers to create bots.
- A set of enhanced features that make interactions between bots and users much simpler.
- An emulator for debugging bots
- A large set of sample bots developers can use as building blocks
- The Bot Builder SDK is an open source SDK that provides everything you need to build great bot experiences using either Node.js or C#.

### Central part of Bot Builder SDK

- **Dialogs** to model conversations and easily manage conversation flow.
- **Form Flow** to streamline the development of bots that collects information of the user.
- **State extensions** such as the development in-memory data storage mechanism or the production-ready table storage adapters.

## The Bot Connector

As the central entry point for bot communication and processes, the Bot Connector handles communication, conversations, state, and authorization for all activities between a bot and its users, including routing messages, managing state, registering bots, tracking user conversations, managing integrated services (such as translation) and even per-user and per-bot storage.

At the most basic level, the Bot Connector facilitates communication between a bot and a user by relaying messages from bot to channel and from channel to bot. Typically, a bot's logic is hosted as a web service, such as an Azure Web App, and, most importantly, has the ability to receive messages from users through the Bot Connector “service”.

**Note** In reality, bot replies are actually sent to the Bot Connector using standard HTTPS POST methods, and are “wrapped” by methods exposed by the Bot Framework.

The Connector also has the task of normalizing messages sent to channels, which makes it easy to develop bots that are platform-agnostic. In Bot Framework-speak, normalizing a message means converting it from the Bot Framework’s schema into the channel’s schema. As an added bonus, in scenarios where a specific channel does not support all aspects of the framework’s schema, the Bot Connector will attempt to convert the message to a format that the channel supports, providing built-in schema “failover”. For example, if a bot sends a message via SMS that contains a "rich" card and action buttons, the Connector will intelligently render the card as an image, then include the actions as links in the message’s text. Pretty cool, right?

## Different Connectors, Different Platforms
The Microsoft Bot Framework Connector is typically just referred to as the Connector, however the specifics of working with the Connector vary based on development language.

In C#, for example, the Connector is accessed via the .NET ConnectorClient:

var connector = new ConnectorClient(new Uri(activity.ServiceUrl));
However, when using Node.js, you have some additional options, since the nature of Node.js is more generic. For example, in Node.js you might use the ConsoleConnector when working in development:

var connector = new builder.ConsoleConnector().listen();
When moving to production (or when testing in a local emulator) you might switch the Node.js ChatConnector scenario, and provide authorization values:

```
var connector = new builder.ChatConnector({
    appId: process.env.MicrosoftAppId,
    appPassword: process.env.MicrosoftAppPassword
});
```

**Note** The ChatConnector requires an API endpoint to be setup within your bot. With the Node.js SDK, this is usually accomplished by installing the Restify Node.js module. The ConsoleConnector does not require an API endpoint.

By implementing this type of universal connection, the Microsoft Bot Framework provides a single REST-based service that enables a bot to communicate across multiple channels such as Skype, Teams, Facebook, and Slack, using a harmonized connector service flow.

## Connector Service Flow

In the Microsoft Bot Framework, the Bot Connector encapsulates every aspect of bot to service communication, and performs virtually all of the “heavy lifting” required for communication between bots and third-party services. In the Microsoft Bot Framework, third-party services are referred to as "channels" and the Bot Connector simply provides the “glue” between the working parts. **In some way it is a bot to rule them all.**


### The Working Parts
Regardless of the simplicity or complexity of a bot implementation, the working parts remain the same:

Your bot logic, written in C# or Node.js
Your bot Web Service, such as an Azure Web App
The Bot Connector, via the Microsoft Bot Framework
User interaction via a third-party service (channel) such as Skype, Slack, or Facebook
Remember, the Connector manages communication, however the Connector does not create the content for communication. The creation of communication content, for example actual messages, is managed by creating and working with activities.

## Activities

In the Microsoft Bot Framework, the Connector uses an activity object to pass information back and forth between a bot and a channel. The term activity is a bit generic, so, in this context, what's an activity? Simply stated, an activity is any event that occurs between a bot and a user, such as an a message being sent, or a notification that something about a conversation has changed.

The most common type of activity is message, but there are other activity types that can be used to communicate various types of information to a bot or channel, such as a conversation update, a contact relation update, or deletion of user data.

The primary, supported activity types are:

- Message: Represents a communication between bot and user.
- Conversation update: Indicates that the bot was added to a conversation, other members were added to or removed from the conversation, or conversation metadata has changed.
- Contact relation update: Indicates that the bot was added or removed from a user's contact list.
- Delete user data: Indicates to a bot that a user has requested that the bot delete any user data it may have stored.
- Typing: Indicates that the user or bot on the other end of the conversation is compiling a response.
- Ping: Represents an attempt to determine whether a bot's endpoint is accessible.
- End of conversation: Indicates the end of a conversation.
- Event: Represents a communication sent to a bot that is not visible to the user.
- Reaction: Indicates that a user has reacted to an existing activity. For example, a user clicks the “Like” button on a message.

In general, most activities are simple notifications reflecting that an event has occurred, and contain little, if any, valuable information, however the message activity type is critical to bot development, as it provides the foundation for all communication content, from simple text strings, to rich, dynamic experience.