# Bot State Options

The Bot Builder Framework enables your bot to store and retrieve state data that is associated with all users, a single conversation, or even a specific user within the context of a specific conversation. State data can be used for many purposes, such as determining where the prior conversation left off or simply greeting a returning user by name. If you store a user's preferences, you can use that information to customize the conversation the next time you chat. For example, you might alert the user to a news article about a topic that interests her, or alert a user when an appointment becomes available.

For testing and prototyping purposes, you can use the Bot Builder in-memory data storage. For production bots, you can implement your own storage adapter or use one of Azure Extensions.


The Microsoft Bot Framework Azure Extensions support the following storage locations:

- Azure Table Storage
- Azure Cosmos DB
- Azure SQL

:bulb: Although used quite frequently in both the documentation and SDK examples, the Bot Framework State Service API is not recommended for production environments, and has been deprecated. It is recommended that you update your bot code to use the in-memory storage adapter for testing purposes or use one of the Azure Extensions for production bots.

Integrating in-memory data storage occurs by spinning up a new MemoryBotStorage object, which might look like this in Node.js:
``` 
var store = new builder.MemoryBotStorage();  
The process would be similar in C#, only using the .NET InMemoryDataStore object instead:

var store = new InMemoryDataStore();
``` 
## Production Storage

Since in-memory data storage is not recommended for production scenarios, it's recommended (and convenient) to use an Azure-based storage mechanism via the Bot Builder Azure Extensions. Transitioning development storage to production storage is really just a matter of using the target storage.

For example, using Azure Table Storage would only change a single line of C# code:

var store = new TableBotDataStore(['YOUR TABLE STORAGE CONNECTION STRING']);
Using Azure Cosmos DB is a little more work, however it's really quite simple:
``` 
var uri = new Uri(ConfigurationManager.AppSettings['YOUR DOCUMENTDB URI']);
var key = ConfigurationManager.AppSettings['YOUR DOCUMENTDB KEY'];
var store = new DocumentDbBotDataStore(uri, key)
``` 
With a bot storage method selected, your code can easily manage state data.

## Manage State Data
- User data: Contains data that is saved for the user on the specified channel. This data will persist across multiple conversations.

- Private conversation data: Contains data that is saved for the user within the context of a particular conversation on the specified channel. This data is private to the current user and will persist for the current conversation only.

- Conversation data: Contains data that is saved in the context of a particular conversation on the specified channel. This data is shared with all users participating in the conversation and will persist for the current conversation only.

-Dialog data: Contains data that is saved for the current dialog only.

Each dialog maintains its own copy of this property.

Using these storage containers makes it easier to persist data based on bot context and scope, for example, storing a current user's information might look like this, in Node.js:
```
session.userData.userName = "Geddy Lee";
session.userData.userAge = 57;
session.userData.hasChildren = true;
```
Retrieving the data is obviously just a standard reversal of values:
```
var userName = session.userData.userName;
var userAge = session.userData.userAge;
var hasChildren = session.userData.hasChildren;
```
Clearing or resetting data, in Node.js, makes sense, too:
```
session.userData = {}; 
session.privateConversationData = {};
session.conversationData = {};
session.dialogData = {};
```