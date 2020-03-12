# FairOrder
Fairorder is the World's First MDaaS  **"Managed Decentralization as a Service"** which is the fastest way  to achieve decentralization using fair ordering of sequence of events. The underlying technology we use is Hedera Hashgraph.
The **fairorder-js-sdk** is the package that will help in integrating our service in your application.

## Installation

### Step 1: Include FairOrder SDK in your project
Download/install our sdk package using npm in your javascript project. The command for the same is:
```ssh
$ npm i --save fairorder-js-sdk
```
### Step 2: Setup developer API credentials
Make sure you are signed in to our web [dashboard](http://dashboard.fairorder.io). You need to create your app using our dashboard which will generate appId and secretId of the respective app. These credentials are important for initializing our sdk. The example for the same is given below.

![](https://fair-order.s3.ap-south-1.amazonaws.com/fo_setup_key.png)


### Step 3: Initialize the SDK 
Then instantiate the sdk object with the app credentials.
```javascript
    const FairOrderSDK = require('fairorder-js-sdk');
    const fairOrder = new FairOrderSDK();
```
Call the init function to initialize the SDK
```javascript
    await fairOrder.init({app_id: "your-app's-app-id", secret_key:"your-app's-secret-key"});
```
### Step 4: Submit your transactions

Call the submitMessage function with channelId and the message to submit.

```javascript
    fairOrder.submitMessage("0.0.195302", "message").then((res)=>{
        console.log('Success::::::', res);
//         res example:::
//         {
//           nodePrecheckcode: 22,
//           receiptStatus: 22,
//           transactionId: 0.0.194939@1584011966.128000000
//         }
    }).catch((error)=>{
        console.log('Error::::::', error);
    });
```

### Table of Contents

-   [FairOrderSDK][1]
    -   [Example][2]
    -   [init][3]
        -   [Parameters][4]
        -   [Example][5]
    -   [getChannelList][6]
        -   [Example][7]
    -   [createChannel][8]
        -   [Parameters][9]
        -   [Example][10]
    -   [updateChannel][11]
        -   [Parameters][12]
        -   [Example][13]
    -   [channelInfo][14]
        -   [Parameters][15]
        -   [Example][16]
    -   [submitMessage][17]
        -   [Parameters][18]
        -   [Example][19]
    -   [getMessageListByChannelId][20]
        -   [Parameters][21]
        -   [Example][22]
    -   [getMessageByMessageId][23]
        -   [Parameters][24]
        -   [Example][25]



## FairOrderSDK

Class represents the entry point of the sdk. By initializing the object of the class the functions are accessible


### Example
```javascript
    const fairOrder = new FairOrderSDK();
```
### init

function to initialize the sdk with app credentials.

### Parameters 
-   `credentials` **[Object][26]** the object containing
    -   `credentials.app_id` **[string][27]** the application id which you get from dashboard
    -   `credentials.secret_key` **[string][27]** the secret key which you get from dashboard

```javascript
    fairOrder.init(credetials).then(()=>{
        console.log('Success::::::');
    }).catch((error)=>{
        console.log('Error::::::', error);

    });
```

### getChannelList

function to get channel list for the application

Returns **[Array][28]** list of channels

#### Example
```javascript
    fairOrder.channelList().then((res)=>{
        console.log('Success::::::', res);
//       res example::::::
//       [
//         {
//           id: '0.0.195302',
//           createdByTransactionHash: '6b65c6b557675a0b0c84058832f7585035872a1810e49380deefeb27db8bea3636277c99737a2635756a340e47b0ef56',
//           createdAt: '2020-03-12T11:03:26.772434Z',
//           creator: '0.0.194939',
//           adminKey: {
//             ed26519: 'e9d22a2f18afb34b5eaf8cc6967d151090c7cafbb9fcbddb87cb5ae4d0a37cb1'
//           },
//           submitKey: { keys: [Array] },
//           memo: 'new-example-channel',
//           autoRenewPeriod: 7890000,
//           autoRenewAccount: '0.0.194939'
//         },
//         {
//           id: '0.0.194960',
//           createdByTransactionHash: '00391c242909274e221b1c2fb733cd99060b4f4a0cd7698824650288a853f158fec00d017dc4e23a14f426d05f992b8b',
//           createdAt: '2020-03-11T14:39:18.222424Z',
//           creator: '0.0.194939',
//           adminKey: {
//             ed26519: 'e9d22a2f18afb34b5eaf8cc6967d151090c7cafbb9fcbddb87cb5ae4d0a37cb1'
//           },
//           submitKey: { keys: [Array] },
//           memo: 'vivek',
//           autoRenewPeriod: 7890000,
//           autoRenewAccount: '0.0.194939'
//         },
//       ]
    }).catch((error)=>{
        console.log('Error::::::', error);
    });
````

### createChannel

function creates a new channel for the provided channel name

#### Parameters

-   `channelName` **[string][27]** refers to name of the channel

Returns **[Object][26]** response obj with transaction receipt

#### Example
```javascript
    fairOrder.createChannel("example-channel-name").then((res)=>{
        console.log('Success::::::', res);
//         res example:::
//         {
//           nodePrecheckcode: 22,
//           receiptStatus: 22,
//           transactionId: 0.0.194939@1584010996.271000000,
//           channelId: 0.0.195302
//         }
    }).catch((error)=>{
        console.log('Error::::::', error);
    });
```


### updateChannel

function to update the name a given channel for the corresponding channelId

#### Parameters

-   `newChannelName` **[string][27]** refers to name of the channel
-   `channelID` **[string][27]** refers to ID of the channel

Returns **[Object][26]** response obj with transaction receipt.

#### Example
```javascript
    fairOrder.updateChannel("new-channel-name", "0.0.195302").then((res)=>{
        console.log('Success::::::', res);
//         res example:::
//         {
//           nodePrecheckcode: 22,
//           receiptStatus: 22,
//           transactionId: 0.0.194939@1584011966.128000000
//         }
    }).catch((error)=>{
        console.log('Error::::::', error);
    });
```

### channelInfo

function to get info for the corresponding channelId

#### Parameters

-   `channelID` **[string][27]** refers id of the channel.

Returns **[Object][26]** channel info response obj.

#### Example
```javascript
    fairOrder.channelInfo("new-channel-name", "0.0.195302").then((res)=>{
        console.log('Success::::::', res);
//      res::::
//         {
//          channelInfo: {
//            topicMemo: 'new-example-channel',
//            runningHash: Uint8Array(48) [
//              0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
//              0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
//              0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
//              0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0,
//              0, 0, 0, 0
//            ],
//            sequenceNumber: 0,
//            expirationTime: Time { seconds: 1591901006, nanos: 772434000 },
//            adminKey: 302a300506032b6570032100e9d22a2f18afb34b5eaf8cc6967d151090c7cafbb9fcbddb87cb5ae4d0a37cb1,
//            submitKey: KeyList { _keys: [Array] },
//            autoRenewPeriod: 7890000,
//            autoRenewAccount: 0.0.194939
//          }
//         }

    }).catch((error)=>{
        console.log('Error::::::', error);
    });

```

### submitMessage

function to submit a message on the corresponding channel

#### Parameters

-   `channelID` **[string][27]** refers to id of the channel
-   `msg` **[string][27]** refers to the message text you want to submit

Returns **[Object][26]** response obj with transaction receipt.

#### Example
```javascript
    fairOrder.submitMessage("0.0.195302", "message").then((res)=>{
        console.log('Success::::::', res);
//         res example:::
//         {
//           nodePrecheckcode: 22,
//           receiptStatus: 22,
//           transactionId: 0.0.194939@1584011966.128000000
//         }
    }).catch((error)=>{
        console.log('Error::::::', error);
    });
```


### getMessageListByChannelId

function to get the list of messages by channelId

#### Parameters

-   `channelID` **[string][27]** refers to id of the channel

Returns **[Array][28]** list of messages on that channel

#### Example
```javascript
    fairOrder.getMessageListByChannelId("0.0.195302").then((res)=>{
        console.log('Success::::::', res);
//       res example::::::
//       [
//         {
//           runningHash: '78648fc4354ee39f29137d156f8b01b9e78ad87450a60f4536e446b2f0f7d57d34c3ca3e9cdb755cbd4a9116bac03a37',
//           sequenceNumber: 1,
//           submittedByTransactionHash: '41e9c97ab1cbceafd2a49db0c5616b82b5b47ad01478018a2b3726796179e7e14b03ff8ec2bef6c2a5cf1ab027a0b426',
//           submittedAt: '2020-03-12T11:30:47.170218002Z',
//           submitter: '0.0.194939'
//         }
//       ]
    }).catch((error)=>{
        console.log('Error::::::', error);
    });
```


### getMessageByMessageId

function to get the message content by message id.

#### Parameters

-   `msgId` **[string][27]** refers to id of the channel
-   `channelId`  
-   `channelID` **[string][27]** refers to id of the channel

Returns **[string][27]** message content of the message id

#### Example
```javascript
    fairOrder.getMessageByMessageId("1","0.0.195302").then((res)=>{
        console.log('Success::::::', res);
//       res example::::::
//       message
    }).catch((error)=>{
        console.log('Error::::::', error);
    });
````


[1]: #fairordersdk

[2]: #example

[3]: #initaccount

[4]: #parameters

[5]: #example-1

[6]: #getchannellist

[7]: #example-2

[8]: #createchannel

[9]: #parameters-1

[10]: #example-3

[11]: #updatechannel

[12]: #parameters-2

[13]: #example-4

[14]: #channelinfo

[15]: #parameters-3

[16]: #example-5

[17]: #submitmessage

[18]: #parameters-4

[19]: #example-6

[20]: #getmessagelistbychannelid

[21]: #parameters-5

[22]: #example-7

[23]: #getmessagebymessageid

[24]: #parameters-6

[25]: #example-8


[26]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object

[27]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String

[28]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array

