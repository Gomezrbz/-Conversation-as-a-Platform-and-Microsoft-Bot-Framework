# Introduction to Bots

One of the most far-reaching and exciting concepts—finally transitioned into mainstream technology discussions—is the Microsoft notion of providing a robust, connected platform for “bridging the gap” between human language and machine intelligence. This concept, referred to as “Conversation as a Platform,” introduces much needed harmony to the boundary between human language and machine intelligence.

"**The entire concept of Conversation as a Platform is about taking the power of human language and applying it universally to computing. At the heart of this platform are bot-conversation bots.**"

To make this effort a reality, Microsoft has introduced a variety of tools, further extending services—originally provided in the Cortana Intelligence Suite—such as developer tools for creating Skype bots, a rich, comprehensive suite of Cognitive Services APIs, and most importantly, the Microsoft Bot Framework—all built on Microsoft's Azure cloud services.

## Bots Everywhere

At a high level, the Microsoft “Conversation as a Platform” vision comprehends the notion of integrating Cortana "personal assistant" services into all devices, as Cortana now runs on Android, iOS (and of course Windows) and then make it easy for Cortana to **be part of as many application experiences as possible,** while being able to understand situational context in messages. However, although on the surface, users are may be interacting with a visible, personal assistant user experience, in reality, Cortana, Siri, and Alexa are really just bots, albeit a super-smart ones.

Microsoft understands that a huge number of these personal assistants (or “digital assistants”) will start working their way into all communication tools, including über-popular services such as Skype, SMS, WeChat, Facebook, Slack and, of course, email. This means the core of "Conversation as a Platform" is really the notion of “Bots Everywhere”.

## Bot Concepts

At its most fundamental level, a bot (a shortened version of the word “robot”) is a term used to describe **a program or process that operates as an agent for a user** (or another program) and attempts to simulate a human activity. However, in the context of "Conversation as a Platform" what we're really talking about is a conversation bot (a.k.a. “chatbot”, "talkbot", “chatterbot”, "Bot", “IM bot”, "interactive agent", or even the unwieldy “Artificial Conversational Entity”. A conversation bot is a computer program, service, or process that conducts a conversation via auditory or textual methods.

**A conversation bot uses decision trees, artificial intelligence and machine learning. In some way they are applications designed for users to interact via natural language understanding insead of a series of manual keyboard or other types of traditional inputs.**

As a rule, conversation bots are designed to convincingly simulate how a human would behave as a “conversational partner”, and thereby pass the infamous Turing test. Many bots use sophisticated natural language processing systems, such as Microsoft's Language Understanding Intelligent Service, however other bot implementations simply scan for keywords within the input, then pull a reply with the most matching keywords, or the most similar wording pattern, from a database.

Either way, bots (or more specifically conversation bots) have quickly becoming an integral part of digital experiences. As part of Microsoft's “Conversation as a Platform”, the Microsoft Bot Framework provides tools for developers to easily create, publish, and manage bot solutions—including automatic translation to more than 30 languages, user and conversation state management, debugging tools, an embeddable web chat control. direct line API methods, and even mechanisms for easy bot discovery.

## Design Principles

The Bot Framework enables developers to create compelling bot experiences that solve a variety of both consumer needs and business challenges. If you are building a bot, it is safe to assume that you are expecting users to use it. It is also safe to assume that you are hoping that users will prefer using a bot experience over alternative experiences like apps, websites, phone calls, and other means of addressing their particular needs. In other words, your bot is competing for users' time against things like apps and websites. So, the real question becomes: how can you maximize the odds that your bot will achieve its ultimate goal of attracting and keeping users? It's simply a matter of prioritizing the right factors when designing your bot.

## Conversation flow

In a traditional application, the user interface (UI) is a series of screens. A single app or website can use one or more screens as needed to exchange information with the user. Most applications start with a main screen, where users initially start their experience, that provides navigation leading to other screens for various functions like starting a new order, browsing products, or looking for help.

Like apps and websites, bots have a UI, but it is made up of dialogs, rather than screens. Dialogs enable the bot developer to logically separate various areas of bot functionality and guide conversational flow. For example, you may design one dialog to contain the logic that helps the user browse for products and a another, separate dialog to contain the logic that helps the user create a new order.

Dialogs may or may not have graphical interfaces. They may contain buttons, text, and other elements, or be entirely speech-based. Dialogs also contain actions to perform tasks such as invoking other dialogs or processing user input.

In a traditional application, everything begins with the main screen. The main screen invokes the new order screen. The new order screen remains in control until it either closes or invokes other screens. If the new order screen closes, the user is returned to the main screen.

### A traditional application flow

In a bot, everything begins with the root dialog. The root dialog invokes the new order dialog. At that point, the new order dialog takes control of the conversation and remains in control until it either closes or invokes other dialogs. If the new order dialog closes, control of the conversation is returned back to the root dialog.

