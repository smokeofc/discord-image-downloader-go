# discord-image-downloader-go
[<img src="https://img.shields.io/badge/Support-me!-orange.svg">](https://www.paypal.me/swk) [![Go Report Card](https://goreportcard.com/badge/github.com/Seklfreak/discord-image-downloader-go)](https://goreportcard.com/report/github.com/Seklfreak/discord-image-downloader-go) [![Build Status](https://travis-ci.org/Seklfreak/discord-image-downloader-go.svg?branch=master)](https://travis-ci.org/Seklfreak/discord-image-downloader-go)

[Download the latest release](https://github.com/Seklfreak/discord-image-downloader-go/releases/latest)

## Discord SelfBots are forbidden!
[Official Statement](https://support.discordapp.com/hc/en-us/articles/115002192352-Automated-user-accounts-self-bots-)
### You have been warned.

This is a simple tool which downloads pictures (and instagram videos) posted in discord channels of your choice to a local folder. It handles various sources like twitter differently to make sure to download the best quality available.

## Websites currently supported
- Discord attachments
- Twitter
- Tistory
- Gfycat
- Instagram
- Imgur
- Google Drive Files and Folders
- Flickr
- Streamable
- Any direct link to an image or video

## How to use?
When you run the tool for the first time it creates a `config.ini` file with example values. Edit these values and run the tool for a second time. It should connect to discords api and wait for new messages.

In case you are using two-factor authentication you have to login using your token. Remove the email and password lines under the auth section in the config file and instead put in `token = <your token>`. You can acquire your token from the developer tools in your browser (`localStorage.token`) or discord client (Control+Shift+I (Windows) or Command+Option+I, click Application, click Local Storage, click `https://discordapp.com`, and find "token" and paste the value).

## How to download old pictures?
By default, the tool only downloads new links posted while the tool is running. You can also set up the tool to download the complete history of a channel. To do this you have to run this tool with a separate discord account. Send your second account a dm on your primary account and get the channel id from the direct message channel. Now add this channel id to the config by adding the following lines:
```
[interactive channels]
<your channel id> = <some valid path>
```
After this is done restart the tool and send `history` as a DM to your second account. The bot will ask for the channel id of the channel you want to download and start the downloads. You can view all available commands by sending `help`.

### Where do I get the channel id?
Open discord in your browser and go to the channel you want to monitor. In your address bar should be a URL like `https://discordapp.com/channels/1234/5678`. The number after the last slash is the channel id, in this case, `5678`. Or, enable Developer mode and right click the channel you need, and click Copy ID.

#### Going to bake into readme later:
OK, Makein found me on discord, so helped him out there. for future readers, here are some instructions:

1. When you've downloaded the files, put the discord-image-downloader-go-windows-amd64.exe file in a folder, let's say 'C:\DiscordDL' for the purposes of this instruction, but you can choose your own location.
2. You will see a command window open and close as it's generating a skeleton config file that you can use to config the selfbot. it will look like so:
```
[auth]
email    = your@email.com
password = your password

[general]
skip edits                           = true
download tistory sites               = false
max download retries                 = 5
download timeout                     = 60
send notices to interactive channels = false

[channels]
channelid1 = C:\full\path\1
channelid2 = C:\full\path\2
channelid3 = C:\full\path\3

[flickr]
api key = your flickr api key

[twitter]
consumer key        = your consumer key
consumer secret     = your consumer secret
access token        = your access token
access token secret = your access token secret
```
change 'send notices to interactive channels = false' to 'send notices to interactive channels = true'
3. fill out your email and password.
4. Create a new section somewhere in the file with the heading [interactive channels], you need that to be able to 'chat' with your secondary account.
5. in a browser, open https://discordapp.com/, and login with your secondary account.
6. You'll be in the DM view, open a chat with your main account, and you'll notice that the URL is something along the lines of https://discordapp.com/channels/@me/873685642264840742.
7. copy the last number from the url and paste it in the config file under [interactive channels], and add a location like so:
```
[interactive channels]
873685642264840742 = C:\DiscordDL\DM
```
8. now you're going to need the id of the channel you want to download from, the easiest way to do so is to enable developer mode. You can do so in either the main client or the browser view by going to the discord settings, under Appearance. After activating it, right click on the channel you want and select Copy ID.
9. Paste it under [channels], and include a download location, like so:
```
[channels]
232143587603644416 = C:\DiscordDL\Server\Channel
```
If you've done as instructed, when you write 'history' (without ') in a DM to your secondary account, you should get the following response:
```
Please tell me one or multiple Channel IDs (separated by commas)
Please make sure the channels have been whitelisted before submitting.
```
Just paste a ID that's already listed under [channels] into the chat, and it should start downloading every image posted to that channel

If you leave the selfbot running, it will automatically download all new images added to all channels listed under [channels], and if you only want to launch it every now and then to update, it seems to ignore pictures that you've already downloaded, so just run the 'history' command again.

Your config.ini should look something like this when you're done:
```
[auth]
email    = mail@mymail.com
password = super1337pw

[general]
skip edits                           = true
download tistory sites               = false
max download retries                 = 5
download timeout                     = 60
send notices to interactive channels = true

[interactive channels]
873685642264840742 = C:\DiscordDL\DM

[channels]
232143587603644416 = C:\DiscordDL\Server\Channel

[flickr]
api key = your flickr api key

[twitter]
consumer key        = your consumer key
consumer secret     = your consumer secret
access token        = your access token
access token secret = your access token secret
```

Hope this helps anyone still having trouble setuping this thing :)
I think this issue can be closed now.
