---
site: https://anypoint.mulesoft.com/apiplatform/popular/admin/#/dashboard/apis/7962/versions/8126/portal/pages/6763/preview
apiNotebookVersion: 1.1.66
title: Slack API notebook
---

```javascript
load('https://github.com/chaijs/chai/releases/download/1.9.0/chai.js');
```

See http://chaijs.com/guide/styles/ for assertion styles

```javascript
assert = chai.assert
```

```javascript
CLIENT_ID = prompt("Please, enter CLIENT ID of your Slack application.")
CLIENT_SECRET = prompt("Please, enter CLIENT SECRET of your Slack application.")
```

```javascript
// Read about the Slack API at https://anypoint.mulesoft.com/apiplatform/popular/admin/#/dashboard/apis/7962/versions/8126/contracts
API.createClient('client', '/apiplatform/repository/public/organizations/30/apis/7962/versions/8126/definition');
```

```javascript
API.authenticate(client,"oauth_2_0",{
  clientId: CLIENT_ID,
  clientSecret: CLIENT_SECRET,
  scope: [
    "identify", "read", "post"
  ]
})
```

```javascript
ACCESS_TOKEN = $4.accessToken
```

Name of channel operated by the notebook

```javascript
channelName = "New Notebook Channel"
```

Lists all channels in a Slack team

```javascript
channelsListResponse = client["channels.list"].get({"token": ACCESS_TOKEN })
```

```javascript
assert.equal( channelsListResponse.body.ok, true )
```

```javascript
channelId = channelsListResponse.body.channels[0].id
```


Fetches history of messages and events from a channel

```javascript
channelsHistoryResponse = client["channels.history"].get({
  "token": ACCESS_TOKEN ,
  "channel": channelId
})
```

```javascript
assert.equal( channelsHistoryResponse.body.ok, true )
```

Gets information about a channel

```javascript
channelsInfoResponse = client["channels.info"].get({
  "token": ACCESS_TOKEN ,
  "channel": channelId
})
```

```javascript
assert.equal( channelsInfoResponse.body.ok, true )
```

```javascript
userID = channelsListResponse.body.channels[0].members[0]
```

Joins a channel, creating it if needed

```javascript
channelsJoinResponse = client["channels.join"].get({
  "token": ACCESS_TOKEN ,
  "name": channelName
})
```

```javascript
assert.equal( channelsJoinResponse.body.ok, true )
```

Invites a user to a channel

```javascript
channelsInviteResponse = client["channels.invite"].get({
  "token": ACCESS_TOKEN ,
  "channel": channelId,
  "user": userID
})
```

```javascript
assert.equal( channelsInfoResponse.body.ok, true )
```

```javascript
leavedChannelId = channelsJoinResponse.body.channel.id
```

Leaves a channel

```javascript
channelsLeaveResponse = client["channels.leave"].get({
  "token": ACCESS_TOKEN ,
  "channel": leavedChannelId
})
```

```javascript
assert.equal( channelsLeaveResponse.body.ok, true )
```

Sets the read cursor in a channel

```javascript
channelsMarkResponse = client["channels.mark"].get({
  "token": ACCESS_TOKEN ,
  "channel": channelId,
  "ts": "1409184000"
})
```

```javascript
assert.equal( channelsMarkResponse.body.ok, true )
```

Sets the purpose for a channel

```javascript
channelsSetPurposeResponse = client["channels.setPurpose"].get({
  "token": ACCESS_TOKEN ,
  "channel": channelId,
  "purpose": "This is the new notebook purpose!"
})
```

```javascript
assert.equal( channelsSetPurposeResponse.body.ok, true )
```

Sets the topic for a channel

```javascript
channelsSetTopicResponse = client["channels.setTopic"].get({
  "token": ACCESS_TOKEN ,
  "channel": channelId,
  "topic": "This is the new notebook topic!"
})
```

```javascript
assert.equal( channelsSetTopicResponse.body.ok, true )
```

Sends a message to a channel

```javascript
chatPostMessageResponse = client["chat.postMessage"].get({
  "token": ACCESS_TOKEN ,
  "channel": channelId,
  "text": "My new notebook message. 4"
})
```

```javascript
assert.equal( chatPostMessageResponse.body.ok, true )
```

```javascript
messageTimestamp = chatPostMessageResponse.body.ts
```

Updates a message

```javascript
// Method not supported.
// chatUpdateResponse = client["chat.update"].get({
//   "token": ACCESS_TOKEN ,
//   "channel": channelId,
//   "text": "Text notebook update.",
//   "ts": messageTimestamp
// })
```

```javascript
//assert.equal( chatUpdateResponse.body.ok, true )
```

Deletes a message


```javascript
chatDeleteResponse = client["chat.delete"].get({
  "token": ACCESS_TOKEN ,
  "channel": channelId,
  "ts": messageTimestamp
})
```

```javascript
assert.equal( chatDeleteResponse.body.ok, true )
```

Lists custom emoji for a team

```javascript
emojiListResponse = client["emoji.list"].get({ "token": ACCESS_TOKEN })
```

```javascript
assert.equal( emojiListResponse.body.ok, true )
```

Lists and filters team files

```javascript
filesListResponse = client["files.list"].get({
  "token": ACCESS_TOKEN ,
  "file": "fileValue"
})
```

```javascript
assert.equal( filesListResponse.body.ok, true )
```

```javascript
fileId = filesListResponse.body.files[0].id
```

Gets information about a team file

```javascript
filesInfoResponse = client["files.info"].get({
  "token": ACCESS_TOKEN ,
  "file": fileId
})
```

```javascript
assert.equal( filesInfoResponse.body.ok, true )
```

Uploads or creates a file

```javascript
filesUploadResponse = client["files.upload"].get({ "token": ACCESS_TOKEN, content : "TestFileContent" })
```

```javascript
assert.equal( filesUploadResponse.body.ok, true )
```

Lists private groups that the calling user has access to

```javascript
groupsListResponse = client["groups.list"].get({ "token": ACCESS_TOKEN })
```

```javascript
assert.equal( groupsListResponse.body.ok, true )
groupId = groupsListResponse.body.groups[0].id
```

Fetches history of messages and events from a private group

```javascript
groupsHistoryResponse = client["groups.history"].get({
  "token": ACCESS_TOKEN ,
  "channel": groupId
})
```

```javascript
assert.equal( groupsHistoryResponse.body.ok, true )
```

Post message to a private group.

```javascript
groupMessageCreateResponse = client["chat.postMessage"].get({
  "token": ACCESS_TOKEN ,
  "channel": groupId,
  "text": "My new notebook message for a private group"
})
```

```javascript
groupMessageTS = groupMessageCreateResponse.body.ts
```

Sets the read cursor in a private group

```javascript
groupsMarkResponse = client["groups.mark"].get({
  "token": ACCESS_TOKEN ,
  "channel": groupId,
  "ts": groupMessageTS
})
```

```javascript
assert.equal( groupsMarkResponse.body.ok, true )
```

Sets the purpose for a private group

```javascript
groupsSetPurposeResponse = client["groups.setPurpose"].get({
  "token": ACCESS_TOKEN ,
  "channel": groupId,
  "purpose": "API Notebook testing."
})
```

```javascript
assert.equal( groupsSetPurposeResponse.body.ok, true )
```

Sets the topic for a private group

```javascript
groupsSetTopicResponse = client["groups.setTopic"].get({
  "token": ACCESS_TOKEN ,
  "channel": groupId,
  "topic": "Testing, testing and, one more time, testing!"
})
```

```javascript
assert.equal( groupsSetTopicResponse.body.ok, true )
```

Lists direct message channels for the calling user

```javascript
imListResponse = client["im.list"].get({ "token": ACCESS_TOKEN })
```

```javascript
assert.equal( imListResponse.body.ok, true )
imListId = imListResponse.body.ims[0].id
```

Fetches history of messages and events from direct message channel

```javascript
imHistoryResponse = client["im.history"].get({
  "token": ACCESS_TOKEN ,
  "channel": imListId
})
```

```javascript
assert.equal( imHistoryResponse.body.ok, true )
```

Post a message to direct channel

```javascript
imMessageCreateResponse = client["chat.postMessage"].get({
  "token": "xoxp-2592965636-2592965640-2593139934-af2baa" ,
  "channel": imListId,
  "text": "My new notebook message for IM 4 (admin)"
})
```

```javascript
imMessageTS = imMessageCreateResponse.body.ts
```

Sets the read cursor in a direct message channel

```javascript
imMarkResponse = client["im.mark"].get({
  "token": ACCESS_TOKEN ,
  "channel": imListId,
  "ts": imMessageTS
})
```

```javascript
assert.equal( imMarkResponse.body.ok, true )
```

Searches for messages and files matching a query

```javascript
searchAllResponse = client["search.all"].get({
  "token": ACCESS_TOKEN ,
  "query": "New notebook query"
})
```

```javascript
assert.equal( searchAllResponse.body.ok, true )
```

Searches for files matching a query

```javascript
searchFilesResponse = client["search.files"].get({
  "token": ACCESS_TOKEN ,
  "query": "New notebook query"
})
```

```javascript
assert.equal( searchFilesResponse.body.ok, true )
```

Searches for messages matching a query

```javascript
searchMessagesResponse = client["search.messages"].get({
  "token": ACCESS_TOKEN ,
  "query": "New notebook query"
})
```

```javascript
assert.equal( searchMessagesResponse.body.ok, true )
```

Lists stars for a user

```javascript
starsListResponse = client["stars.list"].get({ "token": ACCESS_TOKEN })
```

```javascript
assert.equal( starsListResponse.body.ok, true )
```

Lists all users in a Slack team

```javascript
usersListResponse = client["users.list"].get({ "token": ACCESS_TOKEN })
```

```javascript
assert.equal( usersListResponse.body.ok, true )
```