# Bitlbee Mastodon
This document was generated from the help text for the plugin.

Mastodon is a free, open-source social network server. A decentralized solution to commercial platforms, it avoids the risks of a single company monopolizing your communication. Anyone can run Mastodon and participate in the social network seamlessly.

* [register](#register) - Registering an account
* [connect](#connect) - Connecting to an instance
* [read](#read) - Reading your timeline
* [post](#post) - Posting a new status
* [undo](#undo) - Undo and redo
* [context](#context) - Showing a status in its context
* [reply](#reply) - Replying to a status
* [delete](#delete) - Deleting a status
* [favourite](#favourite) - Favouring a status
* [follow](#follow) - Following an account
* [block](#block) - Blocking an account
* [mute](#mute) - Muting an account
* [boost](#boost) - Boosting a status
* [more](#more) - Getting more information about things
* [search](#search) - Searching for accounts and hashtags
* [spam](#spam) - Reporting a status
* [control](#control) - Commands in the control channel
* [hashtag](#hashtag) - Following a hashtag
* [public](#public) - Following the local or federated timeline
* [set](#set) - Settings affecting Mastodon accounts

## register
You need to register your Mastodon account on an *instance*. See https://instances.social/ if you need help picking an instance. It's a bit like picking a mail server and signing up. Sadly, there is currently no way to do this from IRC. Your need to use a web browser to do it. Once you have the account, see *help account add mastodon* for setting up your account.

## set
These settings will affect Mastodon accounts:

* *set auto_reply_timeout* - replies to most recent messages in the last 3h
* *set base_url* - URL for your Mastodon instance's API
* *set commands* - extra commands available in Mastodon channels
* *set message_length* - limit messages to 500 characters
* *set mode* - create a separate channel for contacts/messages
* *set show_ids* - display the "id" in front of every message
* *set target_url_length* - an URL counts as 23 characters
* *set name* - the name for your account channel

## set name
*Type:* string  
*Scope:* account  
*Default:* empty  

Without a name set, Mastodon accounts will use host URL and acccount name to create a channel name. This results in a long channel name and if you prefer a shorter channel name, use this setting (when the account is offline) to change it.

*<kensanata>* account mastodon offline  
*<kensanata>* account mastodon set name masto  
*<kensanata>* account mastodon online  
*<kensanata>* save  

## account add mastodon
*Syntax:* account add mastodon <handle>  

By default all the Mastodon accounts you are following will appear in a new channel named after your Mastodon instance. You can change this behaviour using the *mode* setting (see *help set mode*).

To send toots yourself, just write in the groupchat channel.

Since Mastodon requires OAuth authentication, you should not enter your Mastodon password into BitlBee. The first time you log in, BitlBee will start OAuth authentication. (See *help set oauth*.)

In order to connect to the correct instances, you must most probably change the *base_url* setting. See [connect](#connect) for an example.

## connect
In this section, we'll sign in as *@kensanata@mastodon.weaponvsac.space*. This section assumes an existing account on an instance! Replace username and Mastodon server when trying it.

In your *&bitlbee* channel, add a new account, change it's *base_url* to point at your instance, and switch it on:

*<kensanata>* account add mastodon @kensanata  
*<root>* Account successfully added with tag mastodon  
*<kensanata>* account mastodon set base_url https://mastodon.weaponvsac.space/api/v1  
*<root>* base_url = `https://mastodon.weaponvsac.space/api/v1'  
*<kensanata>* account mastodon on  
*<root>* mastodon - Logging in: Login  
*<root>* mastodon - Logging in: Parsing application registration response  
*<root>* mastodon - Logging in: Starting OAuth authentication  

At this point, you'll get contacted by the user *mastodon_oauth* with a big URL that you need to visit using a browser. See [connect2](#connect2) for the OAuth authentication.

## connect2
Visit the URL the *mastodon_oauth* user gave you and authenticate the client. You'll get back another very long string. Copy and paste this string:

*<mastodon_oauth>* Open this URL in your browser to authenticate: https://.......  
*<mastodon_oauth>* Respond to this message with the returned authorization token.  
*<kensanata>* ****************************************************************  

Once you do that, your login should complete in the *&bitlbee* channel:

*<root>* mastodon2 - Logging in: Requesting OAuth access token  
*<root>* mastodon2 - Logging in: Connecting  
*<root>* mastodon2 - Logging in: Verifying credentials  
*<root>* mastodon2 - Logging in: Getting home timeline  
*<root>* mastodon2 - Logging in: Logged in  

You should now have a channel called *#mastodon.weaponsvsac.space@localhost* where all the status updates and notifications get shown. We'll call this your *account channel*. See *help set name* to change it's name.

Mastodon gives BitlBee a permanent authentication token, which will be saved in your configuration.

You should probably save this configuration.

*<kensanata>* save  
*<root>* Configuration saved  

## read
The default *mode* setting is *chat*. This means that each Mastodon account you add will result in a new channel in your IRC client.

Use *help set mode* in your Bitlbee control channel (*&bitlbee*) to read up on different modes.

## post
The default *commands* setting is *true*. This means that anything you type is a toot unless it looks like command, in which case it is handled as such. In addition to that, you can use the *post <message>* command. If you set the *commands* setting to *strict*, using the *post* command is mandatory.

Use *help set commands* in your Bitlbee control channel (*&bitlbee*) to read up on the various commands.

A well behaved Mastodon client will limit your toots to 500 characters even though the underlying protocols allow for longer messages. By default, Bitlbee does the same. Use *help set message_length* in your Bitlbee control channel (*&bitlbee*) to read up on the hairy details. Basically, some aspects of of your message will count for less: URLs, domain names for mentioned user accounts and the like. See *help set target_url_length* for more information on how URLs are counted.

Note also that Bitlbee itself does word-wrapping to limit messages to 425 characters. That is why longer messages may look like extra newlines have been introduced but if you check the status on the web, you'll see that everything is OK.

## undo
Use *undo* and *redo* to undo and redo recent commands. Bitlbee will remember your last 10 Mastodon commands and allows you to undo and redo them.

Use *history* to see the list of commands you can undo. There is a pointer (*>*) showing the current position.

Use *history undo* if you are interested in seeing the commands that will be used to undo what you just did.

## favourite
Use *fav <id|nick>* to favour a status or the last status by a nick. Synonyms: *favourite*, *favorite*, *like*.

Use *unfav <id|nick>* to unfavour a status or the last status by a nick. Synonyms: *unfavourite*, *unfavorite*, *unlike*, *dislike*.

## context
Use *context <id|nick>* to show some context for a status or the last status by a nick. This will display the ancestors and descendants of a status.

Use *timeline <nick>* to show the most recent messages by a nick.

## reply
If you use the default IRC conventions of starting a message with a nickname and a colon (*:*) or a comma (*,*), then your message will be treated as a reply to that nick's last message.

This only works if that nick's last message was sent within the last 3h. For more information about this time window use *help set auto_reply_timeout* in your Bitlbee control channel (*&bitlbee*).

You can also reply to an earlier message by referring to its id using the *reply <id> <message>* command. The handle of the original author you are replying to will be prepended automatically. It is up to you to mention any of the other people mentioned in the original.

Use *whois <id|nick>* to show handle and full name by a nick, or of all the nicks mentioned in a status.

If you set the *commands* setting to *strict*, using the *reply* command is mandatory.

## delete
Use *del <id>* to delete a status or your last status. Synonym: *delete*.

## favourite
Use *fav <id|nick>* to favour a status or the last status by a nick. Synonyms: *favourite*, *favorite*, *like*.

Use *unfav <id|nick>* to unfavour a status or the last status by a nick. Synonyms: *unfavourite*, *unfavorite*, *unlike*, *dislike*.

## follow
Use *follow <nick|account>* to follow somebody. This determines the nicks in your channel. Verify the list using */names*.

Usually you'll be providing a local or remote account to follow. In the background, Bitlbee will run a search for the account you provided and follow the first match. Sometimes there will be nicks in the channel which you are not following, e.g. a nick is automatically added to the channel when a status of theirs mentioning you is shown.

Use *unfollow <nick>* to unfollow a nick. Synonyms: *allow*.

## block
Use *block <nick>* to block a nick on the server. This is independent of your IRC client's */ignore* command, if available.

Use *unblock <nick>* to unblock a nick.

## mute
Use *mute user <nick>* to mute a nick on the server.

Use *unmute user <nick>* to unmute a nick.

Use *mute <id|nick>* to mute the conversation based on a status or the last status by a nick. Muting a status will prevent replies to it, favourites and replies of it from appearing.

Use *unmute <id|nick>* to unmute the conversation based on a status or the last status by a nick.

## boost
Use *boost <id|nick>* to boost a status or the last status by a nick.

Use *unboost <id|nick>* to unboost a status or the last status by a nick.

## more
Use *url <id|nick>* to get the URL to a status or the last status by a nick.

Use *info instance* to get debug information about your instance.

Use *info user <nick|account>* to get debug information about an account.

Use *info relation <nick|account>* to get debug information about the relation to an account.

Use *info <id|nick>* to get debug information about a status or the last status by a nick.

## search
Mastodon allows you to search for three kinds of things: accounts, hashtags, and the URLs of a status.

Use *search <what>* to get debug information about the things found by a search.

## spam
Use *report <id|nick> <comment>* to report a status or the last status by a nick. Synonyms:*spam*.

Note that the comment is mandatory. Explain why the status is being reported. The administrator of your instance will see this report and decide what to do about it, if anything.

## control
As we said at the beginning, the default *mode* setting is *chat*. This means that each Mastodon account you add will result in a new channel in your IRC client. All the commands mentioned above are what you type in this "instance channel."

There are some standard root commands that only work in the control channel, *&bitlbee*.

## hashtag
This also happens from the control channel, *&bitlbee*.

Here's how to subscribe to *#hashtag* for the account *mastodon*. The *chat add* command takes the parameters *account*, *hashtag*, and *channel name*. In the example we're simply giving the channel the same name. You can name the channel whatever you want. The important part is that the channel *topic* must be the hashtag it is subscribing to.

*<kensanata>* chat add mastodon hashtag #hashtag  
*<kensanata>* channel #hashtag set auto_join true  
*<kensanata>* /join #hashtag  

Don't forget to *save* your config.

Note that where as you can still issue commands in these hashtag channels, the output is going to appear in the original *account channel*.

## public
This also happens from the control channel, *&bitlbee*.

Here's how to subscribe to the *local* or *federated* timeline for the account *mastodon*. The *chat add* command takes the parameters *account*, *timeline*, and *channel name*. In the example we're giving the channel a similar name. You can name the channel whatever you want. The important part is that the channel *topic* must be the name of the timeline it is subscribing to.

*<kensanata>* chat add mastodon local #local  
*<kensanata>* channel #local set auto_join true  
*<kensanata>* /join #local  

Or:

*<kensanata>* chat add mastodon federated #federated  
*<kensanata>* channel #federated set auto_join true  
*<kensanata>* /join #federated  

Don't forget to *save* your config.

Note that where as you can still issue commands in these channels, the output is going to appear in the original *account channel*.

