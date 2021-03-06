# Commands

The bot is a general purpose tracker for all types of robots. You can use it to track any post on any of the sites (meta sites included). The main command which can be used to start reporting posts is the `track` command. It can be invoked in the following manner

     @Boson track sitename trackingType frequency

The complete help and usage of the track command is: 



     usage: track [-d [{HIGGS}]]
                  [-f [{REPUTATION,LENGTH,USER_ID,POST_ID,CONTAINS,TAG,BURNED_TAG,HEAT_DETECTOR} [{REPUTATION,LENGTH,USER_ID,POST_ID,CONTAINS,TAG,BURNED_TAG,HEAT_DETECTOR} ...]]]
                  [-h] [-n [NAME]] [-p [{ONE_BOX,LIST_TAGS,HEAT_DETECTOR}]]
                  [-r [ROOM]] [-t [{STACK_OVERFLOW,STACK_EXCHANGE}]]
                  [-v [VALUE [VALUE ...]]] sitename trackingType frequency

     Argument Parser for the bot.

     positional arguments:
       sitename               Site where the bot has to be run
       trackingType           Type  of  the  tracker  needed.   Can  be  one  of
                              {questions,answers,comments,posts,tags}
       frequency              Frequency of the tracker in seconds

     named arguments:
       -d [{HIGGS}], --dash [{HIGGS}]
                              Set the dashboard to be used by the bot
       -f [{REPUTATION,LENGTH,USER_ID,POST_ID,CONTAINS,TAG,BURNED_TAG,HEAT_DETECTOR} [{REPUTATION,LENGTH,USER_ID,POST_ID,CONTAINS,TAG,BURNED_TAG,HEAT_DETECTOR} ...]], --filter [{REPUTATION,LENGTH,USER_ID,POST_ID,CONTAINS,TAG,BURNED_TAG,HEAT_DETECTOR} [{REPUTATION,LENGTH,USER_ID,POST_ID,CONTAINS,TAG,BURNED_TAG,HEAT_DETECTOR} ...]]
                              Set the filters used by the bot
       -h, --help             Display this message
       -n [NAME], --name [NAME]
                              Give a name to  your  bot  (we  will generate a 10
                              digit value, if you don't)
       -p [{ONE_BOX,LIST_TAGS,HEAT_DETECTOR}], --printer [{ONE_BOX,LIST_TAGS,HEAT_DETECTOR}]
                              Set the printer to be used by the bot
       -r [ROOM], --room [ROOM]
                              Set the room where it has to run
       -t [{STACK_OVERFLOW,STACK_EXCHANGE}], --host [{STACK_OVERFLOW,STACK_EXCHANGE}]
                              Set the chat host of that room
       -v [VALUE [VALUE ...]], --value [VALUE [VALUE ...]]
                              Set the value needed for  the filter, depending on
                              it's type
                             

## Example Usage

Thanks to it being very generic, Boson usually overwhelms users with it's available options, but thankfully most of them are optional. Few sample trackers are:

 - Tracking all the new questions posted on Stack Overflow every 3 minutes (180 seconds)
  
       @Boson track stackoverflow questions 180
       
 - Tracking all the new answers posted on Meta Stack Overflow every 1 hr (3600 seconds) and naming the tracker as `MSO_tracker`
  
       @Boson track meta.stackoverflow answers 3600 --name MSO_tracker
       
 - Tracking the next comment every 500 seconds on PostId 93696 (in this case, a question) on the workplace (highest voted post on that site)
 
       @Boson track workplace comments 500 -f POST_ID -v 93696
 
 - Tracking all the answers every 3000 seconds posted by Shog9 (user 811) on Meta Stack Exchange
 
       @Boson track meta answers 3000 -f USER_ID -v 811 
      
 - Tracking the next featured meta post every 1000 seconds, in room 54445 on chat.stackexchange.com (a private room)
 
       @Boson track meta questions 1000 -f TAG -v featured -r 54445 --host STACK_EXCHANGE
       
 - Tracking recently created tags on interpersonal skills every 21600 seconds. (You can use either the sitename, i.e, "interpersonal" or the entire url "interpersonal.stackexchange.com". Both of them work.)
 
       @Boson track interpersonal.stackexchange.com tags 21600
       
 - Tracking heated comments on The Workplace every 10 minutes, and display it using the Higgs Dashboard. 
 
       @Bos track workplace comments 1500 -f HEAT_DETECTOR -v 5 -p HEAT_DETECTOR -d HIGGS 


## Content types


Boson is still under active development. As of now, the available content types are:

 1. Questions
 2. Answers
 3. Comments 
 4. Posts
 5. Tags
 
 ## Printers
 
 The available printers are:
 
 1. Generic Printer (which is the default option)
 2. One box printer (which one boxes the post by linking it in a separate message)
 
 ## Filters
  
  
 ### Available Filters
 
 The available filters (and the expected values) are:
 
 1. REPUTATION  (The reputation of the poster at which it should be filtered. Should be a number)
 2. LENGTH (The length of the content at which it should be filtered. Should be a number)
 3. POST_ID (The ID of the post on which you need to track comments. Should be a number)
 4. USER_ID (The ID of the user whose posts you need to track. Should be a number)
 5. TAG (The name of the tag which you need to filter the questions. Should be a ; separated list of tag names)
 6. HEAT_DETECTOR (The value of the comment heat at which it should be filtered. Should be a number)
 
 ### Using filters to obtain the data you need
 
 The filters are designed in such a way that you can choose one of them (using `-f` argument) and supply a value (using the `-v` argument), which you use to filter the data you receive. So to get the comments by low reputation users, you can use:
 
      @Boson track stackoverflow comments 100 -f REPUTATION -v -50
      
  Notice the "`-50`" argument supplied as value. When you need something to filter content below the value, use the negative sign. Therefore to track the comments by users with more than 50 reputation, you would be using the same command, excpet with `-v 50`. 
  
  You can add multiple requests as well, for example: 
  
      @Boson track stackoverflow comments 100 -f REPUTATION LENGTH -v -50 -150
      
  would track all the comments that are posted by users below 50 reputation and with a length lesser than 150 characters. The filters can be in any order but make sure that the filter name and its value line up respectively. 
 
