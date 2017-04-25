---
layout: post
title: My BBS Software From 1993
published: true
twitter_plug: true
image: /assets/posts/2017-04-18-my-bbs-software-from-1993/WELCOME.ANS.png
---



The buzz around [Mastodon's](https://mastodon.social/) federated social network has made me nostalgic about bulletin board 
systems in the early nineties. It was an era that is unknown to most people. It was social networking before the phrase existed, and before
giant corporations owned the social networks. Bulletin Board Systems had message boards, private messages, file sharing, and many of the
social features that we are accustomed to in modern web and mobile applications.

I wrote, released and eventually sold my own BBS software called Dementia BBS Software from about 1989 to 1995. Dementia was written in C, and the
source code that it was based on was called WWIV BBS Software. 

Unfortunately I no longer have the source code to Dementia (I would love to see code that I wrote as a teenager!) but was able to locate the zip file distribution from [software.bbsdocumentary.com](http://software.bbsdocumentary.com/IBM/DOS/DEMENTIA/) which is part of [the bbs documentary](http://www.bbsdocumentary.com/).

There is so much that I could say on this topic, but for the sake of this post, I'd like to look at some of the ANSI files that were part of Dementia's distribution. I used an ansi to png coverter written in Go, called [ansigo](https://www.github.com/fcambus/ansigo), to convert them to png files.

<em>Update: This post was front-paged on Hacker News, and you can [see the discussion here.](https://news.ycombinator.com/item?id=14147583) Thanks to everyone on HN for the comments, I enjoyed the conversation!</em>

# The Welcome Graphic

Before logging in with a username and password (or registering as a new user), a user would be presented with a welcome message for the BBS 
that they were on. This was the welcome message for my BBS, The Night Light. It was also the default welcome message for new Dementia installs.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/WELCOME.ANS.png">

# New User Registration

User's filled out a new user profile.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/NEWINFO.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/NEWEDIT.ANS.png">

New User Voting was an optional feature where new users would fill out a form that could be viewed by validated users. Validated
users would then vote on whether or not the user should be granted access, and when a configurable threshold was met, the user would
be auto-validated and given a defined security level. This effectively crowdsourced the process of the SysOp having to review and 
validate new users.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/NUVSCRN.ANS.png">

# Logging on
Logging on required authorization.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/USERBOX.ANS.png">

# Matrix Login
Matrix login was the name of an optional feature where everyone was presented with this menu before logging in, and unvalidated
users could not get past this menu (as opposed to seeing a limited main menu).

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/MATRIX.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/MPWORD.ANS.png">

# The Main Menu
Once logged in, the user was presented with a main menu that would allow them to access other areas of the BBS.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/MAINM.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/MAINP.ANS.png">

# The Time Bank
Users were given an amount of time that they were allowed on the system per day, and could deposit time that they did not use for
the day into a time bank, which could with withdrawed at a later date.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/TIMEBANK.ANS.png">

# Personal User Preferences
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/UCOMMENT.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/PDATAM.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/PDATAP.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/SCREEN.ANS.png">

There were different menu sets (like themes) made by different artists and myself, and also pull down menus.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/MENUTYPE.ANS.png">

# The Messaging System

The text editor for composing public and private messages was full featured.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/EDHELP.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/MSGED.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/TEDIT.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/MSGM.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/MSGP.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/MSGRC.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/MSGRCS.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/MSGSTATS.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/SCANM.ANS.png">


# The File System

The file menu allowed users to upload and download files.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/FANSI.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/FHEADER.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/FILEHDR.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/FILEHDR0.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/FILEM.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/FILEP.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/FILESTAT.ANS.png">

Not all files were online. Some were kept on CDs of shareware, or tape backup. Those were marked as offline, but could 
be requested for me to manually put them online so that they would be available to download.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/OFFLINE.ANS.png">

Batch transfers allowed a queue of files to be downloaded one after the other, or, using the BiModem protocol, files could be uploaded
at the same time that they were being downloaded. Users gained credits by uploading, which could be exchanged for downloading a file 
which cost some number of credits.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/BATCHM.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/BATCHP.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/BATCHST.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/LISTHELP.ANS.png">

You could create a tempory archive from files available to download, and then download that single archive.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/ARCHIVEM.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/ARCP.ANS.png">

Uploaded files were tested to be valid zip files, scanned for viruses, had the FILE_ID.DIZ imported, and Ads removed.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/PRETEST.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/FILETEST.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/ZIPTEST1.ANS.png">

Someone could be a SysOp of the file area, but not other parts of the system.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/FSYSOPM.ANS.png">

# The BBS List

SysOps of other BBSs could add the phone number of their BBS to a directory of BBSs.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/BBSM.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/BBSP.ANS.png">

# Internode Chat
The final version of Dementia supported multi-node operation. It was an extremely beta feature, but it meant that two users could
use the system at one time. I only had one phone line, but using the OS/2 operating system, I was able to run two instances of my BBS
which shared the same data, allowing me to login and use my BBS at the same time as a logged in user. Users logged in across nodes could 
chat with eachother.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/NODEHELP.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/NODELIST.ANS.png">

# The Logoff Graphic

When logging off, right before disconnecting, the user was shown this.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/LOGOFF.ANS.png">

# Miscellaneous

This was the root level SysOp menu, where other administrative areas could be accessed.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/ICONFIG.ANS.png">

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/AUTOM.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/AUTOP.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/AUTOREAD.ANS.png">

A user could page the SysOp, and enter a chat mode with them.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/CHATMENU.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/WHYPAGE.ANS.png">

Most of the strings were customizable and were not hardcoded in the C code.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/CSTYLE.ANS.png">

This was a partial that was used somewhere when a new user logged in. A .VOC media file was played so that the SysOp
knew someone had logged on.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/LOGONVOC.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/NEWS.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/NSCAN.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/STATS.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/SYSOPM.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/UEDIT.ANS.png">
<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/UPLOAD.ANS.png">

# Distribution Docs & Text

Below is the documentation that I included with the zip file download. Dementia allowed you to build custom menus, and one of the 
goals of the documentation was to list the "action codes" that were available for menu items. Each menu item was available to users 
matching a specified security level ranging from 0..255, so permissions could be customized.

The documentation also listed "MCI Codes" which were like template variables (variables that got swapped out for values in menu strings 
or ansi files), listed local keys available to SysOps, and gave thanks to beta testers and distributors, people I swapped code snippets with, 
and people who contributed ansi art.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/DEMENTIA.DOC.png">

By including a file named FILE_ID.DIZ in a zip file, BBS software that supported this standard would include the contents of that file as the 
file description when listing it for download in the file system. This was the FILE_ID.DIZ that was included in Dementia's zip file.

<img src="/assets/posts/2017-04-18-my-bbs-software-from-1993/FILE_ID.DIZ.png">

Those were good times. Good times, indeed.