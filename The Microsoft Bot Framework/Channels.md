# Bot Channels

In bot-speak, a channel is a “conduit” into a third-party service, providing the connection between the Microsoft Bot Framework and user-facing communication apps. Most channels support a core set of bot features, just as sending and receiving plain text messages. Since the Microsoft Bot Framework is designed to allow developers to create platform-agnostic bots, the framework targets all supported channels, and uses the Bot Connector to normalize and harmonize content and messages.

## Bot Channels

The Microsoft Bot Framework currently supports the following 14 channels: Bing, Cortana, Email, Facebook Messenger, GroupMe, Kik, Microsoft Teams, Skype, Skype for Business, Slack, SMS, Telegram, Web Chat, and WeChat.

With such a broad range of third-party channel support, it may seem like all the bases are covered. However, what if your organization needs a rich bot experience integrated into a proprietary system, or you want to take advantage of the Microsoft Bot Framework to surface a bot experience within existing apps and services? Although not really a typical “channel”, per se, the Microsoft Bot Framework supports programmatic access to backend bot services via the Direct Line channel.

## The Direct Line Channel

If you think about channels in practical terms, a channel is really the “app” being used to converse with a bot. As a rule, this is a simple scenario: you deploy your bot to a Skype channel so people can use your bot in Skype. You deploy your bot to a Microsoft Teams channel so people can use your bot in Microsoft Teams. You deploy your bot to a Slack channel so people can use your bot in...wait for it...Slack!

But, what if you want to take advantage of all the benefits of the Microsoft Bot Framework, including the Bot Builder SDK, in your own app? For example, it's quite common for organizations to have “roll your own” solutions spread out across their app landscape, and these solutions are often quite complex, pulling in data and resources from legacy, internal, and even external systems. This is where the Microsoft Bot Framework Direction Line channel fits in, exposing a robust REST-based API you can use to embed your bot into your own apps, webpages, or even server-to-server application—essentially making your own app a supported "channel".

## Client Libraries

Although the underlying services leverage platform-agnostic, REST-based services, as with everything else in the Microsoft Bot Framework, these services are wrapped in client libraries for ease of use in the two most common enterprise development languages: .NET and Node.js. And, like all libraries in the Bot Framework, integrating Direct Line services into an app is simply a matter of installing the language-specific dependencies. To use the Microsoft Bot Framework Direct Line libraries in a:

.NET client: Install the Microsoft.Bot.Connector.DirectLine NuGet package
Node.js client: Install the botframework-directlinejs NPM package

## Authentication
In a standard Microsoft Bot Framework channel, concepts and nuances of authentication are handled by the third-party client itself. Skype bot authentication is driven by a user's Skype account. Facebook Messenger authentication is driven by a user's Facebook account. When using the Direct Line channel, however, clients authentication is obtained with one of the following methods:

A secret: A Direct Line secret is a master key that can be used to access any conversation that belong to the associated bot. Direct line secrets do not expire.

A token. A Direct Line token is a key that can be used to access a single conversation. Direct Line tokens expire, but can be refreshed.

:bulb: A Direct Line secret is used to obtain a Direct Line token.

Deciding between these authentication options really depends on your business and technical requirements. For example, if you're creating a service-to-service application, using a secret is a reasonable and simple approach. However, if you're writing an application where the client runs in a web browser or mobile app, you may want to exchange your secret for a token, where it will limit authorization to the current conversation—and then automatically expire, unless refreshed.

:bulb: Your Direct Line client credentials are different from your bot's credentials. This enables you to revise your keys independently and lets you share client tokens without disclosing your bot's password.

The code you write to perform Direct Line authorization depends on your language of choice. For example, authenication via Node.js could look like this:
``` 
client.clientAuthorizations.add('AuthorizationBotConnector', new Swagger.ApiKeyAuthorization('Authorization', 'Bearer ' + directLineSecret, 'header'));
``` 

In C#, performing authentication is a bit more obfuscated, and would look more like this:
``` 
DirectLineClient client = new DirectLineClient(directLineSecret);
``` 

Either way, the authentication process is ultimately powered by the Direct Line REST-based API.
## Conversations
In the Microsoft Bot Framework, Direct Line conversations are explicitly opened by clients (your apps and services) and can run as long as the bot and client continue participating with valid credentials. While the conversation is open, both the bot and client may send messages, and more than one client can connect to a given conversation—and even participate on behalf of multiple users.

## Activities
Just like any other bot experience, clients and bots exchange several different types of activities, such as message, ping, and typing activities, and as a bonus, the Direct Line API even supports custom activities simply by specifying additional channel data.

Whether you're using Direct Line, or any of the more common third-party channels, bot feature support, especially when it comes to rich media, varies greatly across channels. For example, you can imagine rich media support for SMS messages may be quite a bit different from the support provided by Skype.

As you work through the bot development process, and especially as you make decisions regarding your targeted channels, your best friend will be the Microsoft Bot Channel Inspector.