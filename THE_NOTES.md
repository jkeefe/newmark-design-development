[The Syllabus](./README.md) | [The Fine Print](./THE_FINE_PRINT.html) | [The Notes](./THE_NOTES.html)

# The Notes

Here's where you'll find resources and class notes for every section.

# Getting Started

## Introductions

- A bit about me
    - [Personal website](https://johnkeefe.net)
    - [Work website](https://qz.com)
    - [Quartz Bot Studio](https://bots.qz.com)
    - [Quartz AI Studio](https://qz.com/1464390/)
    - Twitter: [@jkeefe](https://twitter.com/jkeefe)
    - Email: john.keefe (at) journalism.cuny.edu
    - Slack is better! [Here's our Slack](https://cunylab.slack.com).
    
## Products in Journalism

- Products in Journalism preso

- A bit about you
    - Name
    - Where you're from
    - What's your product?

## What's a Prototype (for us)?

- Something you can try
- (Also something you MAKE, which is fun)
- Maybe just *one*
- Not polished
- Not at scale
- Probably not secure
- But TRY-worthy
- Something you can share

### Quick Examples

- SMS bot: `(646) 699-3322`
- Better Weather
- Hot duck: [hotduck.today](http://hotduck.today/)


## Logistics & plan

- Go through the [Syllabus](./README.md).
- The class description, logistics, rules, and grading details are in a document I call "[the fine print](./THE_FINE_PRINT.md)."
- Grading options
- Everyone in the Slack! [Join here](https://join.slack.com/t/cunylab/signup) and use your school email address.

# Playing with APIs

## Make bots to do your bidding

IFTTT - "If this then that" - https://ifttt.com

- Every time Donald Trump tweets, put it in a spreadsheet
- Every time it's at or below 32 degrees send a tweet
- Whenever someone posts on their blog, get an email
- Whenever papers are filed in a court case, get an email 
- Make Alexa tweet for you
- When something happens in the digital world, make something happen in the physical world

## Valuable data is everywhere. Let's get it.

Weather info, crypto prices, earthquake alerts -- it's all available, and ready to be shaped into a new product nobody's made before you did.

- [ProPublica Congressional API](https://projects.propublica.org/api-docs/congress-api/)
- [Dark Sky](http://darksky.net)
- [MTA subway info](http://datamine.mta.info/list-of-feeds)
- [Coindesk Bitcoin API](https://www.coindesk.com/api)

### Dig into some APIs

- Coindesk
    - Deets.
    - API call: [`https://api.coindesk.com/v1/bpi/currentprice.json`](https://api.coindesk.com/v1/bpi/currentprice.json)
    - looks like a mess!
        - Extensions
        - Jsonview
    - Quick discussion of JSON format
        ```json
        
        
        {
            "day": "Wednesday, January 30, 2019",
            "currently": { "description":"SNOW" },
            "forecast": {
                    "condition": "COLD",
                    "temperature": 5,
                    "exclamations": ["Wow!","Brrr!","Careful!"]
                }
        }
        
        
        ```

- Dark Sky API
    - http://darksky.net/dev
    - sign up for an account
    - see your key
    - try your key: [`https://api.darksky.net/forecast/YOUR_KEY_HERE/40.755,-73.991`](https://api.darksky.net/forecast/YOUR_KEY_HERE/40.755,-73.991)
    - toy with the lat/lon
    - Propublica's congressional api
        - https://www.propublica.org/datastore/api/propublica-congress-api
    
- Twilio API
    - Simple script place_call.js (run from my laptop ~/Documents/testing)

## Making quick and dirty dashboards

From web site analytics to stock prices, making dashboards to track your numbers may be the most important product you build, even if just for yourself. We'll use APIs and spreadsheets to make 'em fast.

### Google Spreadsheet Dashboards

- Going to use coinbase.com
- NYC info is: http://api.coinbase.com
- Great dashboard info here: https://www.benlcollins.com/apps-script/beginner-apis/
- Which is also here: https://github.com/benlcollins/apps_script_apis/blob/master/for_website/001_numbers.gs
- We'll add in `JSON.parse(data)` to those examples

Steps:

- Open a new Google spreadsheet
- Name it
- Go to tools -> Script Editor
- Name it
- Copy and paste this block of code into the main window:


```
function onOpen() {

    // this code runs when the spreadsheet is opened
    var ui = SpreadsheetApp.getUi();
    ui.createMenu('API')
      .addItem('Update Bitcoin','callCoinbase')
      .addToUi();
      
}

function callCoinbase() {

    // Call coinbase for the latest data
    var response = UrlFetchApp.fetch("https://api.coinbase.com/v2/prices/spot?currency=USD");

    var coinbase = JSON.parse(response.getContentText());
    var sheet = SpreadsheetApp.getActiveSheet();
  sheet.getRange(1,1).setValue([coinbase.data.amount]);
  
}
```

- Let's review the code
- Reload the page (to trigger the "onOpen" function
- First time it runs, will ask you for permission to use the script. 
- Try the button!

More code snippets:

Add the currency value ...

```
sheet.getRange(1,2).setValue([coinbase.data.currency]);
```

Make it append to the end of the list ... (calculate the "row" as the last row plus 1) ...

```
sheet.getRange(sheet.getLastRow() + 1,1).setValue([coinbase.data.amount]);
```


### Extra info

- Many more great examples here: https://www.benlcollins.com/spreadsheets/starting-gas/


## Roll your own information service

When your project needs to blend existing information, or relies on custom data only you have, you may need to get into some code. We'll use Glitch to play with some examples (no coding experience necessary.)

- Intro to Glitch
    - [Here's my API demo project](https://glitch.com/edit/#!/simple-api-demo?path=README.md:1:0)
    - Show it working
- Data prep
    - The [list of capital data]( https://simple.m.wikipedia.org/wiki/List_of_U.S._state_capitals) I got from Wikipedia.
    - Copy-pasted the table into a text file
    - Search-replaced the commas with blanks to take them out, because they mess things up :-)
    - Saved as a `.tsv` file (tab-separated values). See it [here](https://glitch.com/edit/#!/simple-api-demo?path=capitals.tsv:52:0).
    - use [Mr. Data Converter](https://shancarter.github.io/mr-data-converter/) to convert the `.tsv` data into `JSON - Properties`
    - Copied that into a new file I called [`capitals.json`](https://glitch.com/edit/#!/simple-api-demo?path=capitals.json:50:194)
- Add the state-lookup data part ([available here](https://github.com/jkeefe/cuny-prototyping-lab/blob/master/examples/simple-api-demo/server.js))
- You can remix this!

# Conversational Interfaces

## Build a chatbot

- Walk through [this workshop preso](http://media.johnkeefe.net/chatbot-workshop)

- Intro to Dexter
   - Go to [rundexter.com](http://rundexter.com)
   - Make an account
   - Click "Make your first bot" button (or something similar)
   - Enter your email
   - Pick a password
   - Click "Signup"
   - Click the blue "+ New Bot" button.
   - Name it as you wish (but don't use quotes or apostrophes)
   - For template, Click "Blank Project"
   - Click "Create Bot"
   - Clear out what appeaers (we'll start from scratch for real)

   - `+` is what the human says ... the trigger
   - `-` is what the bot says ... the response
   - Note there's a space after the `+` or `-`

   Let's start out with a good introductory phrase. Let people know right away what they'll get from this bot.

```
   + hi
   - I'm a bot that can answer your questions about Star Island. Ask 
   me anything!
```

   - Try it in the demo phone!


### Triggers and Bot Responses

- `+` is what the human says ... the trigger
- `-` is what the bot says ... the response
- There's a space after the `+` or `-` and before the text that follows.

```
+ hi
- I'm a bot that can answer your questions about Star Island. Ask 
me anything!
```
- I always put a blank line before each new `+` trigger, though it's not actually essential.

- All triggers -- the  `+` lines -- must be **lowercase**
- All triggers -- again, the `+` lines -- should **leave out punctuation**
   - There are some exceptions to this, but they're code-related
   - Pay special attention to apostrophes, commas, question marks, and periods -- leave them out

```
+ whats on star island
- There's a big, old hotel. Also a marine lab, some tennis courts, an old stone chapel and a historical museum. Also lots of seagulls!
```

- There is a single carriage return at the end of a `+` command and at the end of a `-` command.

- Try adding some more questions. 

```
+ where is it
- It's 10 miles off the coast of Portsmouth, New Hampshire.

+ how do you get there
- There are many boats that make regular trips from Portsmouth, New Hampshire.
```

### Catchalls

- An asterisk `*` in a trigger means "anything"

```
+ *
- I'm sorry, I don't understand what you said.
- If that's a question, I don't know the answer yet.
- Ooof. I don't understand. Maybe try asking in another way.
```

### Optionals

Brackets -- `[ ]` -- surround optional content in a trigger. We used this in the "help" trigger:

```
+ [*] help [*]
- Just type a question, and I'll give it my best shot.
```

Let's dissect this a moment, just to be clear:

`+ help` ... matches only the human typing "help" and only "help"; "help me" would not match.
`+ * help *` ... would match only "please help me," because there are words before and after "help"; "help me" would not match.
`+ [*] help [*]` ... matches any mention of "help," no matter if there are words before or after it -- because they are optional. So "help me" matches, as does "help" and "can you please help me?"

### Buttons

Our bot really only answers three questions. So it might make sense to provide buttons to those three things after every question.

To add buttons, use the "button" button, which looks like a share icon at the top of your scripot. Position your cursor at the end of the introduction text and click the button button. Then edit the script to look like this: `^buttons(Location, Getting There, What's on Star)`

**Important:** Now we have to go change the triggers for those questions to these titles. That's because clicking a button basically mimics the user _typing_ the content of the button.

So:

```
+ where is it
- It's 10 miles off the coast of Portsmouth, New Hampshire.
```

... becomes ...


```
+ location
- It's 10 miles off the coast of Portsmouth, New Hampshire.
```

As you change the trigger names for your answers, be sure to remember: all lowercase, no punctuation

Try it!

### Routing

You'll quickly note that to keep getting answers you have to say `hi`. It would be nice to have all of the buttons show up after every answer.

To do that, _could_ add buttons after every answer, like so:

```
+ location
- It's 10 miles off the coast of Portsmouth, New Hampshire. ^link("https://goo.gl/maps/T5qxWXTXLLF2","Star Island Map") ^buttons(Location, Getting There, What's on Star)
```

But there's a better way. 

Let's make a new trigger called `my buttons` that contains just the buttons:

```
+ my buttons
+ ^buttons(Location, Getting There, What's on Star)
```

And then _route_ the user to that trigger after every option. We do that with the `{@ trigger}` notation, like so:

```
+ hi
- I'm a bot that can answer your questions about Star Island. What 
would you like to know about? {@ my buttons}

+ location
- It's 10 miles off the coast of Portsmouth, New Hampshire. ^link("https://goo.gl/maps/T5qxWXTXLLF2","Star Island Map") {@ my buttons}

+ getting there
- There are many boats that make regular trips from Portsmouth, New Hampshire. ... like the Thomas Laighton ^image("http://media.johnkeefe.net/class-modules/boat.jpg") {@ my buttons}

+ whats on star
- There's a big, old hotel. Also a marine lab, some tennis courts, an old stone chapel and a historical museum. Also lots of seagulls! {@ my buttons}

+ [*] help [*]
- Here are the things I know how to do. Just pick one! {@ my buttons}
```

This may seem silly, but it solves two things: You don't repeat yourself (which coders call _DRY_ code) as much, and if you happened to add a fourth or fifth option, you'd just change one line instead of several.

### Adding fun features

Add a picture ...

```
+ how do you get there
- There are many boats that make regular trips from Portsmouth, New Hampshire. ... like the Thomas Laighton ^image("http://media.johnkeefe.net/class-modules/boat.jpg")
```

You can also add a link!

```
+ where is it
- It's 10 miles off the coast of Portsmouth, New Hampshire. ^link("https://goo.gl/maps/T5qxWXTXLLF2","Star Island Map")
```

These "shortcuts" -- what Dexter calls the commands that start with a carrot `^` aren't something you have to memorize. They're also available in the bar above your bot script by clicking the little gray pictures just above your script.

You can also use add buttons to "help" to make that better ...

```
+ [*] help [*]
- Here are the things I know how to do. Just pick one! ^buttons(Location, Getting There, What's on Star)
```

### Order matters

When someone types something to your bot, RiveScript will go through your bot script top to bottom until it hits a match.

```
+ hi there
- Hi friend!

+ hi there
- This response would never be seen.
```

This is also why we put "catchall" functions at the end.

### "Pick one" from a response list

- If you have multiple `-` lines after a `+` trigger, RiveScript will pick one of the `-` lines at random.

```
+ tell me a cat fact
- Cats have four legs.
- Cats belong to the Felidae family.
- Dogs have owners, cats have servants.
```

### Publish your bot

To get this ready to share, click the green "Publish Topic" button.

Dexter is great about walking you through this entire process, under the "Platforms" button. 

- To start, click on the "Platforms" button.
- Choose Website.
- Click the large block of code in the middle of the screen. It'll get copied to the clipboard.

![Click on web block](../module-build-a-chatbot/images/web_code.png)

We're going to put this code onto the web using a paste service. 

- Go to [pste.eu](http://pste.eu).
- Click into the big box.
- Paste the code into the box.
- Hit "Submit"
- You'll get private link. Click it!
- It looks like you now have a blank screen, but click the icon in the lower-right corner.
- Your chat bot will appear!
- Try it!


### Share it with others

You can allow other people to try your bot by giving them your _pste.eu_ link. 

(Also you may want to bookmark it at this point.)

### Adding "News" or other live info to your bot

Dexter (and almost every bot platform) lets you incorporate API calls into your bot. The full documentation is here, but let's try a quick example.

We'll get the current price of 1 Bitcoin in dollars using this Coinbase api call, which doesn't require a key: `https://api.coinbase.com/v2/prices/spot?currency=USD`

This returns JSON that looks like this:

```json
{
    "data": {
        "base": "BTC",
        "currency": "USD",
        "amount": "3884.895"
    }
}
```

Note that using "dot notation," the value we want here is `data.amount`.

In Dexter, you can get this info with this code:

```
+ whats a bitcoin in dollars
$ GET https://api.coinbase.com/v2/prices/spot?currency=USD
- The current price of one bitcoin is ${{data.amount}} dollars.
```

Again, for more details and more complicated data handling, s[ee the Dexter documentation](http://docs.rundexter.com/writing/advanced/http-requests/). 

### What if you have several bot questions where the answer could be "yes" or "no"

Best to do that with **topics**, which are [described in the Dexter Docs here](http://docs.rundexter.com/writing/basics/topics/).

## Alexa, what's a digital assistant?

Voice interfaces are popping up everywhere, and it's possible they will be key to information acquisition in the months and years to come. We'll use Dexter to build an Alexa Skill.

### Examples

- Cat facts
- Weather
- Do I need an umbrella
- Better weather
- Flash briefing audio
- Flash briefing bot voice 

### The making of

- Alexa's architecture
- Anatomy of an Alexa skill
- Better weather

### Make one with Dexter

- Start a new bot in Dexter
- Make the first trigger `+ launchrequest` and provide a friendly introduction. This will be the entry point for your bot script.
- Make the second trigger `+ factlist` and provide a list of facts. Remember, if there are multiple responses beginning with `-`, one will be picked at random.
- Here's an example you can just copy-and-paste into your Dexter bot script:

```
+ launchrequest
- Here's your Star Island fact: {@ factlist}

+ factlist
- Star Island is 10 miles off the coast of Portsmouth, New Hampshire.
- The hotel on the island is called "The Oceanic."
- There is no natural fresh water reserves on the island. Fresh water is collected from arriving boats, rainwater and a seawater desalination system.
- The pirate Blackbeard visited once and is said to have left both treasure and his wife on the neighboring island.
```

We also need a "farewell" section to close out our Alexa session, using the shortcut: `^alexaEndSession(true)`

```
+ farewell
- You will come back. You will come back. Have a great day. ^alexaEndSession(true)
```

Finally, we need to direct every response to the farewell trigger with `{@ farewell}` at the end of every line. (If you don't, Alexa will "hang" and leave the blue ring alive. Say "Alexa, quit" to escape).

So:

```
+ factlist
- Star Island is 10 miles off the coast of Portsmouth, New Hampshire. {@ farewell}
- The hotel on the island is called "The Oceanic." {@ farewell}
- There is no natural fresh water reserves on the island. Fresh water is collected from arriving boats, rainwater and a seawater desalination system. {@ farewell}
- The pirate Blackbeard visited once and is said to have left both treasure and his wife on the neighboring island. {@ farewell}
```

- You can also check out my [full example script](https://github.com/jkeefe/workshops/blob/master/module-alexa-fact-skill/alexa-example.rs).
- Click the "Publish Topic" button to make sure your edits stick!

### Wiring up Alexa

- If you're not already registered as an Amazon Developer, do that first. In a new tab, go to [developer.amazon.com](https://developer.amazon.com) and sign up. 
    - Provide the information requested
    - When asked to log in, you can use the Amazon account you use to shop on Amazon (if you do).
    - If you have an Amazon Alexa device already, it's a lot easier down the road if you use the Amazon account (and email address) associated with that device.
    - When asked, say you're not going to collect money for your work. (You can change this later.)
    - Once logged in and ready to go, click on "Alexa Skills Kit," either mid-page or from the "Alexa" tab at the top of the page.
- Head back to your bot on Dexter
- Chose "Platforms" from the menu at the top of the screen (the paper airplane icon).
- Chose "Alexa"
- From here, you should [follow the instructions on this page](http://docs.rundexter.com/platforms/alexa/deploy/). Here are some important notes on that:
    - **Skip Step 4**, and instead go to Step 5, which is the option to use a "catch-all" mode.
    - In Step 5, the instructions should say to click "Build Model" -- which is the button you need to click.
    - In Step 9, you "deploy" your bot from the Dexter Console. Look near the top of the page for the tiny switch that currently says "undeployed" and flip it.

One "gotcha" that affects lots of students: Be sure that your bot topic is _published_, too. To check that, o back to the "Edit" page (the pencil icon) and click "Publish Topic."

- Test it out!

### Don't have an Alexa device handy?

Back in the Alexa tab of your browser, click to the "Test page" where you can "Enter Utterance" to test how Alexa will respond. If you allow access to your computer microphone, you can also click the microphone icon and just _talk_ to it as you would an Alexa device.

You can see how Alexa will respond in the "Service Response" section, or you can _hear_ the response by clicking on the "Listen" button below the "Service Response" window.

### If you have an Alexa device matching your developer account

If you Alexa Developer Account matches the account with which you registered your Alexa device, just say the invocation phrase! In my example, it would be "Alexa, open Star Island facts."

Note that if the blue ring gets stuck "on," it probably means you forgot to use `^alexaEndSession(true)` as the last thing in your script.

### Troubleshooting

- Makes sure you've chosen (and saved) an invocation phrase and that the phrase doesn't contain any blocker words.
- Make sure the invocation phrases match on Alexa and Dexter
- Click "save model" and "build model"
- On the Dexter "Deploy" page (the airplane), make sure the little switch at the top is flipped from "undeployed" to "deployed"
- On the Dexter "Edit" page (the pencil) make sure your bot is "Published" with the green button. 

### To invite others to try (or invite another Alexa device not tied to your dev account)

To beta test on an actual Alexa device:

- Must have **all** of the green checkmarks checked. 
- That includes a 108x108 and a 512x512 px logo.
- Invite beta testers 
- If the Amazon account you're using for development is not the one you use for your Alexa device, then you need to invite yourself at the address you use for the device, too.
- Beta testers visit http://alexa.amazon.com ... and should eventually get a pop-up inviting them to participate
- Then the skill gets added.

## Dexter Docs

[More information here](http://docs.rundexter.com/writing/advanced/alexa/)!

## Prototyping voice conversations
 
Building a whole Alexa skill just to test it out on your friends or possible customers is possible -- but not always necessary. We'll learn how to prototype voice conversations quickly using an audio playboard.

Try the [Quartz Alexa Playboard example here](https://playboard-template.glitch.me/).

Check out the [code for the playboard here](https://glitch.com/~playboard-template). You can click "remix" to make your own copy to play with.

Read more about how to build this playboard in the [Quartz Bot Studio blog post](https://bots.qz.com/986/relatively-rapid-prototyping-for-voice/) about it.

## Storytelling with chatbots

Texting or chatting with bots is one way to communicate with your audience. We'll learn the dos and don'ts of automated conversations -- and then we'll make one.

- Here we'll draw from the second half of my [Eyeo 2018 presentation](https://vimeo.com/287093921).

# Machine Learning at Play

## Say what? Computers understanding human language

Automatically processing what someone is saying -- either in a chat, to a voice assistant, or in an email -- is increasingly possible thanks to machine learning. We'll play with one of these natural language processing tools (Dialogflow) to get a handle on how to make it work for you.

### Utterances

Also called "Training Phrases" (Dialogflow).

Those are all the things a human might say that mean the same intent. So: 

- Wow
- OMG
- whoa!
- I can't believe it!
- Amazing

... could all _utterances_ for an intent we might call the `chitchat-wow` intent. The more utterances, the better the NLP learns.

### Intents

Having your bot (or any conversational software) understand "yes" is pretty clear. But what if people say yes differently?

- Yes!
- Yup.
- You bet!
- Si.
- Of course

You can teach it that _phrases like this_ mean "yes." So we could call this intent `chitchat-yes`.

- No way
- Nope
- nada
- no
- Heck no

If we see words like the above, we could say these are `chitchat-no`.

- Wow
- OMG
- whoa!
- I can't believe it!
- Amazing

And words like these could mean the `chitchat-wow` intent.

So you could make bot responses to those _intents_ instead of those words, and let the Natural Language Processor decide which intent is, um, intended.

### Training

Interestingly, most natural language systems allow you to review its decisions and _train_ it when it performed well and performed poorly.

## More intents

Consider the intents for the following phrases:

- What's the forecast in Minneapolis tomorrow?
- Will it rain in New York Friday?
- What's the temperature outside?
- Do I need an umbrella?

## Entities

To answer a "forecast" intent, you need two additional pieces of information: Where and when. 

These are called "entities" (and also slits and elements and probably many other things).

So a `weather-forcast` intent requires `place` and `time`.

- What's the forecast in Minneapolis tomorrow?
    Intent: `weather-forecast`
    Entity Place: `minneapolis`
    Entity Time: `tomorrow`
    
- Will it rain in New York Friday?
    Intent: `weather-precipitation`
    Entity Place: `new york`
    Entity Time: `friday`

- What's the temperature outside?
    Intent: ?
    Entity Place: ?
    Entity Time: ?

- Do I need an umbrella?
    Intent: ?
    Entity Place: ?
    Entity Time: ?

- Dialogflow in console
- Using as an API
- Dexter

### Slots

Slots are a category of Entity. So `city` is a slot, and `minneapolis` is the entity.

### Actions

In Dialogflow, you can name an "action" in addition to an intent. The action is the name of something that should be done. It can be passed along to your code.

## Dialogflow + Dexter

## Introduction to Dialogflow

There are lots of tools out there to use. We'll play with [Dialogflow](https://dialogflow.com) (which used to be called API.ai ... so there may be some notations here that still reference that).

## Setup

As usual, you'll need to sign up. It's free. And you'll need a Google/Gmail account.

- Click "Sign up for Free"
- Log in with Google (Dialogflow is a Google product).
- Choose "Create Agent" -- and you may need to authenticate with Google again here.
- Note that you can think of "Agents" as one bot brain. What you teach one agent isn't (easily) shared with another agent.
- Name it "MyAgent" (no spaces allowed)
- Leave the "Link to Google Project" line empty and hit OK
- Check the `V1 API` button (note that Version 1 won't work after October 2019)
- Click "Save"

OK, your "agent" is established.

- If you don't see a sidebar on the left side, click the menu icon (the three horizontal lines)
- In the sidebar, click on "Small Talk."
- You'll get a new screen. Look for the "Enable" switch and turn it on
- Click "Save"

You have now turned on a bunch of default responses for common things humans say to bots.

You can alter the default responses on this page, tho it would take you a while to go through them all.

Try typing some things in the "Try it now" space in the upper right corner.

Note that these defaults do **not** result in an _intent_. That's because we haven't made them yet. They **do** however, result in an _action_ ... which we can use in our code.

## Play a little

Find the "Try it now" box at the top and try typing some random phrases that might constitute small talk. What happens?

Pay close attention to the "Intent" and "Action" areas.

Also try things that might be casual synonyms for "yes" and "no."

Be sure to check out the 

## Connect it to your Dexter Bot

- On the Dialogflow settings page, copy the "Client Access Token"
- Switch to your Dexter bot
- Paste the "Client Access Token" at the very top of your bot script.
- In front of the token, add `! var apiai = Bearer ` so it looks something this:

```
! var dialogflowkey = Bearer ab12cd34ef56ab78cd90ef12
```

- Copy the code below and paste it to the bottom of your bot script:

```
+ *
$ GET https://api.dialogflow.com/v1/query?v=20150910&query=<call>encode_uri <star></call>&lang=en&sessionId=<get _platformId> {"headers":{"Content-Type":"application/json", "Authorization": "<bot dialogflowkey>"}}
- The action I detect is: ${{result.action}}


> object encode_uri javascript
    return encodeURIComponent(args[0])
< object
```

- OK! Now try saying some things into the sample phone on the Dexter console.

## Handle calls for help

Let's be sure that whenever someone says help, they get a kind response:

```
+ help
- I'm sorry you're having trouble!
- I'll try to get you some help!
```

Try it in the phone simulator!

But what about "Can you assist me?" For that, let's handle anything the natural language thinks is a call for help, or `smalltalk.agent.can_you_help`.

- Copy this line ...

```
* ${{result.action}} == smalltalk.agent.can_you_help => {@ help}
```

- ... and paste it in your "catchall" trigger as the second-to-last line. Like this:

```
+ *
$ GET https://api.dialogflow.com/v1/query?v=20150910&query=<call>encode_uri <star></call>&lang=en&sessionId=<_platformId> {"headers":{"Content-Type":"application/json", "Authorization": "<bot dialogflowkey>"}}
* ${{result.action}} == smalltalk.agent.can_you_help => {@ help}
- The action I detect is: ${{result.action}}
```

We've added an "if-then" statement to the block. It says: If `${{result.action}}` is equal to `smalltalk.agent.can_you_help` then go to a `help` trigger.

See it there?

Try it!

Note that anything _other_ than help ends up at the last line, which the bot uses.

## Got nothin'? Use Dialogflow's answer

Remember when you use Dialogflow in the testing box and it actually provides an answer? We can use that. It's 
`${{result.fulfillment.speech}}`. (I know this, because I clicked on the "Show JSON" button in API.ai and can see what would be sent back to our bot!)

So let's replace the last line of our messy code block with that. Instead of 

```
- The action I detect is: ${{result.action}}
```

use ...

```
- ${{result.fulfillment.speech}}
```

So now your covered ... pretty much.

Only issue remaining is that if the bot doesn't recognize anything it sends back blankness. So let's tweak the final lines in the "catchall" block one last time, pasting in:

```
+ *
$ GET https://api.dialogflow.com/v1/query?v=20150910&query=<call>encode_uri <star></call>&lang=en&sessionId=<_platformId> {"headers":{"Content-Type":"application/json", "Authorization": "<bot dialogflowkey>"}}
* ${{result.action}} == smalltalk.agent.can_you_help => {@ help}
* ${{result.fulfillment.speech}} != "" => ${{result.fulfillment.speech}} 
- Sorry, I have no idea what you just said.
```

Those last two lines are: If the "speech" line is not equal (`!=`) to blankness (`""`) then respond with the "speech" line.

If not, we get the last line. You can add more of these `-` lines to add variety.

## Starting from scratch?

What we just built is a good starter script, incorporating the natural language processing for catching strangeness and letting you build from scratch. If you'd like to start over, start from [this file](https://github.com/jkeefe/workshops/blob/master/module-chatbot-add-nlp/a-good-start.rs).

# Image recognition

## Google Vision API

Let's see it at work with the [drag-and-drop](https://cloud.google.com/vision/docs/drag-and-drop) example.

But for a computer to do it, we need an API key. This is not simple, but let's make it happen:

- Go to https://cloud.google.com/
- Sign in to the console with your Google account
- Create a new project, which is probably either a button or a dropdown next to the words "Google Cloud Platform"
- Give it any name, and complete the new-project process
- In the sidebar, click on "APIs & Services"
- At the top of the screen, click "+ ENABLE APIS AND SERVICES"
- Search for "Vision"
- Click on "Cloud Vision API"
- Click "Manage" (or add?)
- In the sidebar, choose "Credentials"
- At the top of the page, choose "+ Create Credential"
- Click the radio button for "No, I'm not using them"
- Click "What Credentials do I need"
- Enter a service account name (I called mine "picture-checker")
- Use the "Select a role" dropdown. I picked Project > Viewer
- Key type is JSON
- Click "Continue"
- You will likely download a file you should put in a safe place
- Now use the dropdown "Create Credentials" and pick "API Key"
- You should see your API Key. Copy that to the clipboard.
- Click "CLOSE"
- Whew!

OK, let's go over to the [Glitch Google Vision demo](https://glitch.com/~google-vision-demo) I made. 

- Click "Remix This" to make your own copy.
- First off, go into the `.env` file and paste your API key right after `GOOGLE_VISION_API_KEY=` (no space)
- While you're here, type a phrase you'll remember after `SEKRIT_URL_KEY` (but don't use spaces)
- Click on `server.js` and I'll walk you through the code.

## Sometimes a duck is a special duck

Can you teach a computer to recognize the Mandarin duck in Central Park. Yup. Is that useful? Could be! We'll learn how, as we see how image processing and machine learning can work together on your project.

## Using Clarifai

The "hot duck" is all the rage. Let's get a computer to identify it.

- Sign up for an account at https://clarfai.com
- Click "Create New Application"
- Name it "duck-finder"
- Click "Create APP"
- In the row of your app, click on the "Explore" eye
- Here's where I uploaded a bunch of pictures of the Mandarin Duck. This can take a moment while the system processes all of the pictures you've uploaded.
- Click the lower-left corner of each image to engage the check-mark on each one
- Click the "+ Add Concepts" button at the bottom
- Call the concept "hotduck"
- Click "ADD"
- Leave the checkbox checked to create a new model
- Click "Done"
- Hover over the name of the model and three dots appear •••
- Click the ••• and chose "Train Model"

For the fun of it, click on one of the images. See that Clarifai knows what the images are, generally, and also that it's been tagged "hotduck" by you.

- In the upper-right corner of the screen, click on your name and then "Settings"
- Click on "API Keys"
- Copy the API key for your app to the clipboard

OK, now we're going to use the model.

- Head over to the [Glitch Demo](https://glitch.com/edit/#!/clarifai-demo) I built.
- Make your own copy by clicking "Remix to Edit"
- Select the `.env` file
- Paste your API key right after the equals sign in `CLARIFAI_API_KEY=` (no spaces)
- Write a short phrase you can remember right after `SEKRIT_URL_KEY=` (but again, no spaces)

Take a look at the `server.js` file and also the `assets` directory.

Try putting different urls from the `assets` directory after the `image_url` on line 29.

To send that image to Clarifai and view the results, click on the "Show" button and then add the "short phrase you can remember" after the url there.

Try all of the images in `assets`. Do you see an issue?



# Good Product Stuff

## Lots of innovation is happening in email. Yes, email.

A good email offering may be the most important product for your project. We'll look at what makes some emails great and also how to use tools to send **useful** emails programmatically. 

## Physical products: Leaving the laptop for the tabletop

Tiny computers can sense the environment or respond to your commands. They can even keep track of things when you're far away. Prototyping these kinds of products is surprisingly cheap and easy. We'll do it in class.

## Data security: Yours, your company's, your customers'

Let's talk about security. We'll get into how you can start practicing better personal security and about how to act responsibly and ethically with the data you get from others.

## Real-world production in the cloud

When it's time for your prototype to become production-worthy, you'll need scale, security, and reliability. And chances are, that means putting it in a "cloud" service like Amazon's AWS -- or the similar offerings from Google, Microsoft, and others. We'll take a tour through AWS so you can better coordinate with your engineers when it's time to go big
