 [The Syllabus](./README.md) | [The Fine Print](./THE_FINE_PRINT.html) | [The Notes](./THE_NOTES.html)

# The Notes

Here's where you'll find resources, code, links, and notes for every class. Materials are added here generally at least one day before each class, but can change and get updated up until class time.

<a name="class1"></a>

# Class 1 • Basic internetting

## Introductions

- A bit about me
    - [Personal website](https://johnkeefe.net)
    - [Work website](https://qz.com)
    - [Quartz Bot Studio](https://bots.qz.com)
    - [Quartz AI Studio](https://qz.ai/)
    - Twitter: [@jkeefe](https://twitter.com/jkeefe)
    - Email: john.keefe (at) journalism.cuny.edu
    - Slack is better! [Here's our Slack](https://socialjournalism2019.slack.com).
    
## Products in Journalism

- Presentation: Overview of products in Journalism

- A bit about you
    - Name
    - Where you're from
    - What's your Social J area of interest?

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

- SMS bot: Text "hi" to `(646) 699-3322`
- Better Weather
- Hot duck: [hotduck.today](http://hotduck.today/)

## Logistics & plan

- Go through the [Syllabus](./README.md).
- The class description, logistics, rules, and grading details are in a document I call "[the fine print](./THE_FINE_PRINT.md)."
- Everyone in the Slack! [Join here](https://join.slack.com/t/cunylab/signup) and use your school email address.

## Exploring web pages

- Sign up for [Glitch](https://glitch.com)
- Make a new project > `hello-webpage`

## Assignment

_This is the "Class 1" assignment. Do it now ... it's due on at high noon before Class 2._

Start a new `hello-webpage` project in Glitch and make it your own. Change colors, play with formatting, play with the text. Get creative! Google around for html tips and tricks if you want. Post the link to your project in Slack in `#design-dev` so we can all try it.

<a name="class2"></a>

# Class 2 • Roll your own information service

## Quick review of last week

- Some submissions 
- Fixes

### Note on "assets"

- This is where we can put images and other things
- Add an image to the assets
- Use the full url to add it to `index.html` using `<img src = "[URL OF IMAGE]" >` 
- (note image tag is one of the few in html without a closing tag. so no `</img>`.

## A little more advanced Internetting

- Search for `jkeefe` or go to [https://glitch.com/@jkeefe](https://glitch.com/@jkeefe)
- Find `newmark-bark` (do this again, even if you did last week -- it's a new version)
- Remix it!
- Name it `[yourname]-bark`

## A different structure

### "Static"

What we did last week:

1. **Request:** You -> https://curious-scout.glitch.me -> Glitch
2. **Response:**  Glitch -> `index.html` -> you

### Static, but server-driven

 Instead of Glitch just serving up your fixed or *static* html page (as in Class 1) you're using a "server" file that serves up the page.

1. **Request:**  You -> https://newmark-bark.glitch.me -> Glitch
2. **Response:**  Glitch -> `server.js` -> `index.html` -> you

### Dynamic

1. **Request:**  You -> https://newmark-bark.glitch.me/random -> Glitch
2. **Response:**  Glitch -> `server.js` -> get data -> inject data -> `fact-page.html` -> you

### Dynamic with a database

1. **Request:**  You -> https://newmark-bark.glitch.me/bella -> Glitch
2. **Response:**  Glitch -> `server.js` -> query a database -> get the answer -> turn into JSON -> you


## Let's get some dog data

- Let's look at a [CSV of 81,000 NYC dogs](https://docs.google.com/spreadsheets/d/1dvL1vq4YTG4Y72XHlWvwTg27f1k3UVnXDZfJm5MHef8/edit?usp=sharing)

## Databases!

- Go to the Glitch console
- Change directory into the `.data` directory by typing `cd .data`
- To get the CSV, type this `wget "http://media.johnkeefe.net/class-modules/nyc_dogs_2012.csv"`
- To start the database, type `sqlite3 dogs.db`
- To switch into CSV mode type `.mode csv`
- To import the CSV into our database, type `.import nyc_dogs_2012.csv doginfo`
- Note that ^ that line created a "doginfo" table within our database
- Check out if everything worked by typing: `.schema doginfo`

### A little bit of SQL

- Try `SELECT * FROM doginfo LIMIT 10;` (note the `;` at the end of a SQL command)
- Try `SELECT dog_name, count(dog_name) FROM doginfo GROUP BY dog_name;`
- Try `SELECT dog_name, count(dog_name) FROM doginfo GROUP BY dog_name COLLATE NOCASE;`
- Try `SELECT dog_name, count(dog_name) FROM doginfo GROUP BY dog_name COLLATE NOCASE ORDER BY count(dog_name);`
- Try `SELECT dog_name, count(dog_name) FROM doginfo GROUP BY dog_name COLLATE NOCASE ORDER BY count(dog_name) DESC LIMIT 10;`
- Try `SELECT dog_name, count(dog_name) FROM doginfo WHERE dog_name LIKE "bella" GROUP BY dog_name COLLATE NOCASE;`

## Data on the web

- Let's look at the `index.html` file
- A little bit about JSON
- To make your life easier, download JSONview plug in

## Assignment

_This is the "Class 2" assignment. Do it now ... it's due on at high noon before Class 3._

Add a new "route" to your web service that, when hit by a web browser, displays a list of the top 5 dog breeds (by count) in the database. Paste a link to that route into Slack.

<a name="class3"></a>

# Class 3 • Texting as a service

## Review last class

- Based on a URL, we can get number of dogs named X (or count of breeds)
- Remember ...
    - the URL comes in to Glitch
    - it gets routed to `server.js`
    - based on the format of the url, we do different things
    - for example, we can pick out the name "spot" from `.../name/spot`
    - then we check the database
    - then we display the count (or total)

## Walkthrough: Handling texts with Twilio

Twilio is a service that accepts text messages (also phone calls!) and sends them on to a web service -- like Newmark Bark!

Here's the path: 

    - **Request:** Your phone > the service phone number > Twilio > Our Glitch site
    - **Response:** Our Glitch site > Twilio > your phone number > your phone 
        
If you send "hello" the service phone number, here's what Twilio sends to our Glitch site:

```json
{
    "ToCountry": "US",
    "ToState": "NY",
    "SmsMessageSid": "SM184eed5c374485f10ef379ec9a2e2259",
    "NumMedia": "0",
    "ToCity": "NEW YORK CITY",
    "FromZip": "10010",
    "SmsSid": "SM184eed5c374485f10ef379ec9a2e2259",
    "FromState": "NY",
    "SmsStatus": "received",
    "FromCity": "NEW YORK",
    "Body": "hello",
    "FromCountry": "US",
    "To": "+1929xxxxxxx",
    "ToZip": "",
    "NumSegments": "1",
    "MessageSid": "SM184eed5c374485f10ef379ec9a2e2259",
    "AccountSid": "ACxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "From": "+1917xxxxxxx",
    "ApiVersion": "2010-04-01"
}
```

### Quick digression: GET vs POST

- ^^ That bunch of data is a little unwieldy to put in a URL. 
- There's another way to get data to a website: the POST request (and it's often upper-case!)
- One URL, and a "package" of data
- This is available to us as the `request.body` variable
- So the message is `request.body.Body` ... which is "hello"

We'll use "POST" requests in our project.

## Replying to Twilio

First we have to accept incoming POST messages. So I added this "route" to `server.js` in my original Glitch app (note that this goes just above the line that reads "listen for requests :)" ):

```javascript
app.post('/text/name', function(request,response) {
  
  var data = {} // no data yet
  response.render('text-back.html', data)
  
}) 
```

To send back a message to Twilio, there's a special little language that Twilio uses (they call TwiML), which looks like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Response>
    <Message>Hello back!</Message>
</Response>
```

[The Twilio documentation has more about this](https://www.twilio.com/docs/sms/twiml), if you ever need to explore it.

I've stored exactly that code above as `views/text-back.html` in my Glitch app.

We send that back to Twilio in our Glitch app just like we did with the `fact-page.html`

## Let's get more sophiticated

Remember ... `request.body` is all of our text data ... and `request.body.Body` is the message itself. So we can use that in our code.

So we can get all of the message, and pass the name into the database.

I'll step through what you'll do.

## Your turn

### Preparing the Glitch side:

- Cut and paste this code into your Glitch app. **Note that this goes just above the line that reads "listen for requests :)":**

```javascript
app.post('/text/name', function(request,response) {
  
    console.log(request)
  
    db.all('SELECT dog_name, count(dog_name) AS total FROM doginfo WHERE dog_name LIKE "' + request.body.Body + '" GROUP BY dog_name COLLATE NOCASE', function(err, rows) {
    
    if (err) {
      console.log(err)
    }
    
    var data = rows[0]
    console.log(data)
      
    response.render('text-back.html', data)
    
  })
  
}) 
```

- Make a new file called `views/text-back.html`
- Paste this code into your new file:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Response>
    <Message>There are {{total}} dogs by that name!</Message>
</Response>
```

### Set Up Twilio

We'll be using [Twilio](http://twilio.com) to make the connection between the telephone systems and your code.

- Open a new browser tab
- Go to [Twilio](http://twilio.com)
- "Sign up" to make a free trial account.
    - Use: SMS
    - Project: SMS Surveys
    - Language: node.js
    - Under 10,000 uses per month
- Enter the number of the cell phone you have with you
    - This will only be used for verification
    - You won't (and, in fact, can't) "send" from your personal number
    - Can check the box to avoid being called
- Enter verifcation number
- "Get a Number"
- "Choose this number"
    - Mine is (347) 768-7183
    - AKA +13477687183
- Trial account set up!
    - Your trial account has $14.50 remaining
    - Trial accounts can only send messages to verified numbers in these countries
    - Messages sent in trial will begin with "Sent from a Twilio Trial Account"
    - While you have a trial account, you're limited to one Twilio number
    
- Send incoming requests to Glitch;
    - Click on the phone number
    - Scroll down to "Messaging"
    - Note the box that says "A MESSAGE COMES IN"
        - Set it to "Webhook"
        - Paste into the box `https://[YOURNAME]-bark.glitch.me/text/name`
        - HTTP POST
        - SAVE!
        
- Try sending "spot" to your phone number!

_This is the "Class 3" assignment. Do it now ... it's due on at high noon before Class 4 (Which is THURSDAY)._

Add a the new "route" to your web service that so that when I text your phone number I get the right number of dogs. Make sure it works and post a screenshot of your interaction with your bot into Slack.

<a name="class4"></a>

# Class 4 • Introduction to conversational interfaces

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

These are called "entities" (and also slots and elements and probably many other things).

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

### Actions

In Dialogflow, you can name an "action" in addition to an intent. The action is the name of something that should be done. It can be passed along to your code.

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
- Check the `V2 API` button.
- Click "Save"

OK, your "agent" is established.

- If you don't see a sidebar on the left side, click the menu icon (the three horizontal lines)
- In the sidebar, click on "Small Talk."
- You'll get a new screen. Look for the "Enable" switch and turn it on
- Click "Save"

You have now turned on a bunch of default responses for common things humans say to bots.

You can alter the default responses on this page, tho it would take you a while to go through them all.

Try typing some things in the "Try it now" space in the upper right corner.

Note that these defaults do **not** result in an _intent_. That's because we haven't made them yet. They **do** however, result in an _action_ which we can use.

## Play a little

Find the "Try it now" box at the top and try typing some random phrases that might constitute small talk. What happens?

Pay close attention to the "Intent" and "Action" areas.

Also try things that might be casual synonyms for "yes" and "no."

## Assignment

_This is the "Class 4" assignment. Do it now ... it's due on at high noon before Class 5 (Which is a week from Monday)._

"Hi, I'm Newmark Bark! Ask me anything about dogs and dog ownership in New York City!"

- Write three asks -- questions or requests, in regular English, that someone might ask in response to this prompt.
- Make then questions nobody else has posted in Slack already!
- For each question ...  
  - describe the "intent" of the question.
  - identity any "entities" in the question. 
  - identify any "missing entities" you'd need to know to answer the ask. 

Here's an example:

- Ask: How much is a plane ticket from New York to Miami?
- Intent: plane-ticket-price
- Entities: departure city, destination city
- Missing entities: departure date, destination date

<a name="class5"></a>

# Class 5 • Talk to me: Making a voice service for Google Home

## Giving Dialogflow more smarts

Remember, last class we taught Dialogflow to (mostly!) identify the dog name in the natural language phrase, "How many dogs are named spot?". But it didn't *answer* the question. 

To answer the question, we need to ask our special service -- which lives in Glitch! Let's set up Glitch to answer the question.

## Updating our Glitch project to fulfill the requests

Dialogflow is going to send us a "fulfillment request." If you'd like to see the whole "payload" it will send, [look at the documentation here](https://cloud.google.com/dialogflow/docs/fulfillment-how#webhook_request
).

The key piece we're going to want is the "dogname" value, right? We need to know the name of the dog to look up. That's represented by this value in the payload: `queryResult.parameters.dogname`

So this is the code we'll add to the `server.js` file in our Glitch app. Remember to paste this on a blank line above the "// listen for requests :)" line!

```
app.post('/voice/name', function(request, response){
  
  var search_dog = request.body.queryResult.parameters.dogname 
  
  db.all('SELECT dog_name, count(dog_name) AS total FROM doginfo WHERE dog_name LIKE "' + search_dog + '" GROUP BY dog_name COLLATE NOCASE', function(err, rows) {
    
    if (err) {
      console.log(err)
    }
    
    var total_dogs
    
    if (rows.length < 1) {
      total_dogs = "no"
    }  else {
      total_dogs = rows[0].total
    }
    
    var response_phrase = `There are ${total_dogs} dogs named ${search_dog} in New York City.`

    var data ={
      "fulfillmentText": response_phrase
      }

    response.send(JSON.stringify(data))
    
  })
  
})
```

We'll walk through this in class. It should be mostly familiar!

Important fix: We also need to change line No. 9 in the Glitch script.

Delete: 

```
app.use(bodyParser.urlencoded({ extended: true }));
```

And replace it with:

```
app.use(bodyParser.json())
```


## Add fulfillment to our intent

- Back in Dialogflow ... 
- In the side menu, click on "Fulfillment"
- Across from "Webhook" click the "enable" switch
- In the "URL" field, put this url, substituting your Glitch project name:
    - `https://[yourproject].glitch.me/voice/name/`
- Click "Save"

Now we have to go back and get this intent set up for being "fulfilled" this way:

- In the side menu, click "Intents"
- Click on the `dog-name-count` intent
- Scroll all the way down "Fulfillment"
- `Enable webhook call for this intent`

## Wiring it up to Google Assistant (and Google Home)

### Quick updates we'll need for Dialogflow

- Add information to the Welcome intent
    - Because we need a welcome!
- Add an "action" to our dog name intent. Call it `get-dog-name`

### Need to tie that to one of the "Actions by Google"

- Go to <a href="https://console.actions.google.com">`console.actions.google.com`</a>
- Pick `New Project`
- Agree and continue (if you agree!)
- Look for your "agent" name (probably `dog-name-count`) in the list of projects, and pick that
- On the "Welcome to your new project" page, scroll down and pick `conversational`
- Enter a "Display Name" -- this is a public-facing name your users would ask for. So if you put "Doctor Dog" here, users would say, "OK, Google. Talk to Doctor Dog."
- Pick a Google Assistant voice if you'd like to change it

### Head back to Dialogflow

- Click on `Integrations`
- Click on `Integration Settings`
- Add an "Implicit invocation" -- the dog name intent you made
- Click the switch for "Auto-preview changes"
- Click "Test"

### Testing in Actions by Google

- Try the text chat!
- Click on the microphone and enable permission to use your microphone
- Try it!

You can also get here from Dialogflow by clicking "See how it works in Google Assistant"

## Deployment (aka: Making it available to others)

You can make Google Assistant apps available to others, either a select group of testers or to the public at large. Here is a good post outlining [the steps for doing that](https://medium.com/heptagon/chapter-12-how-to-build-a-google-home-app-with-dialogflow-app-deployment-9596bd74d9ad).

## Assignment

_This is the "Class 5" assignment. Do it now ... it's due on at high noon before Class 5 (Which is a week from WEDNESDAY)._

Show me that you've successfully connected Dialogflow to your Glitch service, and that you get a correct answer when you ask "How many dogs are named spot." We'll do this in class. Make sure I watch you do it individually.

If you can't do this in class, or were not in class, use [QuickTime to make a screen recording](https://support.apple.com/guide/quicktime-player/record-your-screen-qtp97b08e666/mac) of you using it and DM that recording to me in Slack.

<a name="class6"></a>

# Class 6 • Storytelling with chat & voice

## Tips for crafting story flow 

[Watch this video](https://vimeo.com/287093921) ... which is essentially the class presentation.

## Build a bot using Dexter

We'll step through the [slides for today's class](http://media.johnkeefe.net/chatbot-workshop/assets/player/KeynoteDHTMLPlayer.html#24).

## Assignment

_This is the "Class 6" assignment. Do it now ... it's due on at high noon before Class 7._

Go through the [Build-a-Bot workshop using Dexter](http://media.johnkeefe.net/chatbot-workshop/assets/player/KeynoteDHTMLPlayer.html#24) and publishing all of your topics to the web. Then **paste the `pste.eu` url for your bot into Slack.**

That's it! If you get errors, hit me up in Slack. Give yourself time to work on it and debug it. 

<a name="class7"></a>

# Class 7 • Make bots to do your bidding

We'll particularly focus on automated bot tools for journalists.

## Anatomy of a bot

- Trigger
- Response

## Google Alerts

Make a [Google alert](https://www.google.com/alerts) for stories and people, especially when you're working on them.

What's the trigger? What's the response?

## Klaxon

- Setup: https://github.com/themarshallproject/klaxon
- John's: https://qz-klaxon.herokuapp.com/

## IFTTT

- weather
- alexa -> tweet
- hashtag to Slack
- RSS court cases
    - Pacer: https://www.pacer.gov/psco/cgi-bin/links.pl
- trump tweets
- any hashtag you're interested in
- something on a cron
- web hooks
- sms text

## Zapier

- https://zapier.com/

## Introduction to APIs

- Newmark Bark
    - https://newmark-bark.glitch.me/name/spot

- Coinbase
    - Deets.
    - API call: https://api.coinbase.com/v2/prices/spot?currency=USD
    - Downloads a file

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
    

## Putting it into Dexter!

```
+ whats a bitcoin worth
$ GET https://api.coinbase.com/v2/prices/spot?currency=USD
- The current price of one bitcoin is ${{data.amount}} dollars.
```

## Assignment

Make an IFTTT recipe, take a screenshot of the rule and that you've toggled it to "Connected" and post that screenshot in Slack.


<a name="class8"></a>

# Class 8 • APIs and the people who love them

## Making a "Meiers" quake Tweeter

### Challenge

- Here's the [origin video](https://www.youtube.com/watch?v=PaAKnWtCQZs)
- Here's the [site I made converting magnitude-moment scale to Meiers](https://meier-quake.glitch.me/)

Task: **I want to make a twitter bot that sends out a tweet whenever there's an earthquake, but says the strength in meiers**



### Helpful code snippets

IFTTT formula payload
```
{"title": "{{EntryTitle}}", "content": "{{EntryContent}}", "url": "{{EntryUrl}}" }
```

Typical title:
```
M 1.7 - 22km NNW of North Nenana, Alaska
```

Regex
```
/^M (.*) - (.*)$/
or
/^M (.*?) - (.*)$/
```

### Regular expressions!

Amazing, arcane "searching on steroids."

- [Rubular](https://rubular.com/)
- [The bastard's book of regular expressions](http://regex.bastardsbook.com/files/bastards-regexes.pdf)

### Tweeting from Glitch

- Searched Glitch and found [this example Glitch project](https://glitch.com/edit/#!/twitterbot?path=README.md:1:0).
- Here's info on [setting things up on the Twitter side](https://botwiki.org/resource/tutorial/how-to-create-a-twitter-app/).

## Assignment: Imagine a twitter bot you want to make. Then how would you make it. 

Imagine a twitter bot you want to make. Then how would you make it. Answer these questions in the #design-dev Slack channel: 

- What is the trigger?
- What does the response look like? (Show me a sample)

- where's the data come from?
- what does the data look like?
- what do you need to do with the data
- what is the flow

_This is the "Class 8" assignment. Do it now ... it's due at high noon before Class 9._

<a name="class9"></a>

# Class 9 • Making Supercharged Spreadsheets

## Google Spreadsheet Dashboards

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
- Reload the page (to trigger the "onOpen" function)
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

## Airtable "Base" and their API


### Start a spreadsheet

- Head over to [airtable.com](https://airtable.com).
- Start a new "base"
- Then make a few entries
- Delete any blank entries

### Check out its custom API

- Then head over to the api section at [api.airtable.com](https://airtable.com/api)
- Pick the same "base."
- Click "show api key" at the top right
- Then copy the url (not the `curl` part) from under "Example Using Query Parameter"
- Open a new tab in your browser and paste that in

### Use it for Glitch

- Open new tab for your Glitch project
- Put `AIRTABLE_API_KEY="YOUR_API_KEY"` in to your `.env` file for your "bark" project
- Replace `YOUR_API_KEY` with your actual API key from the Airtable tab, enclosed in quotes.
- In the Glitch app, we need to add the "airtable.js" library to this project, which you do by altering the `package.json` file and it's "dependencies" section to look like this (adding a comma and the "airtable" line):

```json
"dependencies": {
    "express": "^4.16.3",
    "mustache-express":"^1.2.8",
    "sqlite3": "^4.0.0",
    "airtable": "^0.7.2"
  },
 ```

- Back on the Airtable tab, click "JavaScript" at the top
- Then we add this code to the top of the project, copied from the airtable api code. Note I've changed it from `YOUR_API_KEY` to `AIRTABLE_API_KEY`. (Your code will be slightly different, because your "base" has a different ID.)

```javascript
var Airtable = require('airtable');
var base = new Airtable({apiKey: process.env.AIRTABLE_API_KEY}).base('appSNJkE8AsR2E1EX');
```

- Let's add this as a new "view" called `news.html`
- I duplicated `fact-page.html` and called it `news.html`. Here's the code:

```html
<html lang="en">
  
  <head>
    <title>Newmark Bark</title>
    <meta name="description" content="latest news">
    <link id="favicon" rel="icon" href="https://glitch.com/edit/favicon-app.ico" type="image/x-icon">
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- import the webpage's stylesheet -->
    <link rel="stylesheet" href="/style.css">  
  </head>
  
  <body>
    <h1>
      Newmark Bark • Latest News
    </h1>
    <h2>
      {{fields.Name}}
    </h2>
    
    <p>
      {{fields.Notes}}
    </p>
  </body>
  
</html>
```

- Then I added this code to the `server.js` file, just above the line that says `// listen for requests`:

```JavaScript
app.get('/news', function(req, resp) {
  
  base('Headlines').select({
    view: 'Grid view'
    }).firstPage(function(err, records) {
    
      if (err) { 
        console.error(err)
        return
      }

      var last_record_number = records.length - 1

      var data = records[last_record_number]

      // Whenever you change your templates (those files in views/) you need to
      // change this number to clear the data cache and reload the templates
      data.cachebust = 10

      // pass the data to the html template and serve up the page
      resp.render('news.html', data)

  })
  
})
```

## Assignment

_This is the Class 9 assignment._

Make the Coinbase-fed Google spreadsheet as described above, and post a screenshot of it working in Slack. 

<a name="class10"></a>

# Class 10 • Intro to AI for journalism

Here's [a PDF with today's slides](https://www.dropbox.com/s/stqo1ngtbmdufwf/Class10-AI-Intro-Images.pdf?dl=0).

Other key links:
- [Google Vision API](https://cloud.google.com/vision/), including a live demo
- [Google Colab Notebooks](https://colab.research.google.com)
- Steps for [using the Quartz AI Studio notebooks](https://github.com/quartz/aistudio-workshops)
- The video describing [how to get a Google Vision API key](https://drive.google.com/file/d/18eh27UlIYHAdYNGupWChyBabuJ3aKA5E/view?usp=sharing)

## Assignment

Use the [Google Vision API demo](https://cloud.google.com/vision/) (mid-page where it says "Try the API") and drag a picture into the box. Take a look at the results in each tab, and post into Slack a screenshot of your most interesting result.

<a name="class11"></a>

# Class 11 • Bespoke machine learning for sorting text

We're back in [Google Colab Notebooks](https://colab.research.google.com).

We used two notebooks this class. For the first exercise: 

- go to [Google Colab Notebooks](https://colab.research.google.com)
- pick `Github`
- type `Quartz` and enter
- pick the notebook titled `gg-sort-tweets-with-fastai.ipynb`

For the second exercise:

- go to [Google Colab Notebooks](https://colab.research.google.com)
- pick `Github`
- type `Quartz` and enter
- pick the notebook titled `ii-extracting-entities-plus-similarity.ipynb`

## Assignment

You got lucky because I forgot to incorporate the assignment into the lesson as I had planned ... so everyone gets assignment credit for this class.

<a name="class12"></a>

# Class 12 • Sensors & Physical computing: From the laptop for the tabletop

Here's a PDF of the [slides for this class](https://www.dropbox.com/s/o5aq7lkzgsne9pv/Class12-Sensors.pdf?dl=0).

## Assignment

With a class partner, successfully build the liquid-conductivity sensor! If you are not in class this day, arrange with me to build it another time (must be during or before Class 15). 

<a name="class13"></a>

# Class 13 • AMA: Journalism Grab Bag

## Automation

- [Slide deck is here](https://www.dropbox.com/s/ck5j868xnk8k9kt/Class13-Automation.pdf?dl=0)
- [Addressing micro-audiences at scale](https://drive.google.com/file/d/1CJvITDxHEbPKMUO4Pq457N8BvuEZHrGk/view)
- [EngagedCitizens.us](https://engagedcitizens.us/#meeting-archive)

## Digital investigations

### Brooklyn Voter Purge (WNYC)

- [60,000 Fewer Democrats in Brooklyn and No Clear Reason Why](https://www.wnyc.org/story/democratic-voter-rolls-drop-more-60000-brooklyn-presidential-primary/?utm_source=local&utm_medium=treatment&utm_campaign=daMost&utm_content=damostviewed)
- [De Blasio Demands Explanation, as Decline in Registered Brooklyn Voters Doubles](https://www.wnyc.org/story/de-blasio-demands-explanation-boe-drops-126000-brooklyn-democrats)
- [Brooklyn Voter Purge Hit Hispanics Hardest](https://www.wnyc.org/story/brooklyn-voter-purge-hit-hispanics-hardest/)
- [Board of Elections Returns Purged Brooklyn Voters to Rolls](https://www.wnyc.org/story/board-elections-returns-purged-brooklyn-voters-rolls/)
- [City Board of Elections Admits It Broke the Law, Accepts Reforms](https://www.wnyc.org/story/city-board-elections-admits-it-broke-law-accepts-reforms/)

### Political Ads (Quartz)

- [Political Ad Collector](https://projects.propublica.org/political-ad-collector/)
- [Facebook Ad Library](https://www.facebook.com/ads/library/)
- [Current Trump Ads](https://www.facebook.com/ads/library/?active_status=active&ad_type=all&country=US&impression_search_field=has_impressions_lifetime&view_all_page_id=153080620724)
- [Trump is using impeachment to collect new supporters with Facebook ads](https://qz.com/1735875/trump-is-using-impeachment-to-collect-new-maga-fans-on-facebook/)

### Interrogating Black Boxes (ProPublica)

- [Minority Neighborhoods Pay Higher Car Insurance Premiums Than White Areas With the Same Risk](https://www.propublica.org/article/minority-neighborhoods-higher-car-insurance-premiums-white-areas-same-risk)
- [Machine Bias: There’s software used across the country to predict future criminals. And it’s biased against blacks.](https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing)

### Investigation tools

- See this [fabulous slide deck from ONA](https://www.slideshare.net/onlinenewsassociation/digital-forensics-using-social-and-online-tools-to-find-great-stories-ona19) (In class, we'll start with Jane Lytvynenko on slide 31.)
- Or the [full video here](https://livestream.com/accounts/26035773/events/8806759/player?width=640&height=360&enableInfoAndActivity=true&defaultDrawer=&autoPlay=true&mute=false).

## Tips for working with newsroom developers & designers

- Get them involved early: at the idea/notion stage
- Collaborate with them as the journalists they are (not as a service desk)
- Aim to build something that does *one thing well*
- Brainstorm ideas with them
- Be prepared to do the data digging, finding, FOIA-ing
- Work out a system where *you* clean the data (you'll get more insights!)
- Otherwise work on the project *together* when possible
- Be clear about your hopes and goals for the final result
- Avoid "fishing expeditions" (ie: "Can you see if there is a story here?")
- Related: Avoid "data dumping" on your audience (ie: "Do you see a story here?")
- Be patient
- Watch for places where you're fine skipping certain features
- Be firm about places where you are not

- If you need help on your own code ...
    - Make sure to use a "linter" to check for typos
    - Try to frame the problem in a tweet (the act of doing so can help solve the problem and/or zero in on it)
    - Be sure to Google the problem first (someone else has had this issue, too)
    - Be clear about what you've already tried
    
## Assignment 

Try three of "Jane's tools and resources" ([on slide 49 of this deck](https://www.slideshare.net/onlinenewsassociation/digital-forensics-using-social-and-online-tools-to-find-great-stories-ona19)) to get a feel for how they work. Post a screen shot of something interesting you found using each tool (so three images total) into the shared Slack channel. Due by noon on December 9, 2019.


