 [The Syllabus](./README.md) | [The Notes](./THE_NOTES.html)

# The Notes

Here's where you'll find resources, code, links, and notes for every class. Materials are added here generally at least one day before each class, but can change and get updated up until class time.

<a name="class1"></a>

# Class 1 • Basic internetting

## Introductions

- A bit about me
    - [Personal website](https://johnkeefe.net)
    - [Quartz AI Studio](https://qz.ai/)
    - Twitter: [@jkeefe](https://twitter.com/jkeefe)
    - Email: john.keefe (at) journalism.cuny.edu
    - Slack is better! [Here's our Slack](https://socialjournalism2020.slack.com).
    
- A bit about you
    - Name
    - Where you're from
    - What's your Social J area of interest?
    
## Engagement Projects in Journalism

- Overview of engagement projects in journalism
    - [KPCC/LAist Coronavirus Answers](https://laist.com/2020/04/17/can-you-get-coronavirus-from-tap-water-faucet-sewage.php)
    - [ProPublica's Get Involved page](https://www.propublica.org/getinvolved)
    - [First Draft SMS course](https://firstdraftnews.org/latest/course-training-us-election-misinformation/)
    - Electionland Bot ... pick a method:
        - Text VOTE, VOTA (for Spanish), or 投票 (for Chinese) to 81380
        - Message us at 1 850 909-8683 on WhatsApp
        - or visit [Electionland on Facebook Messenger](https://m.me/electionland)

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
    - [The Skill](https://www.amazon.com/Really-Good-Smarts-LLC-Weather/dp/B07BRF678K/)
    - [The Source](https://forecast.weather.gov/MapClick.php?lat=40.74913000000009&lon=-73.99236000000002#.X0e8OtNKjOR)

## Logistics & plan

- Go through the Syllabus.
- Everyone in the Slack! [Join here](https://socialjournalism2020.slack.com) and use your school email address. Use channel **#design-development**.

## Exploring web pages

- Sign up for [Glitch](https://glitch.com)
- Make a new project > `hello-webpage`

## Assignment

_This is the "Class 1" assignment. Do it now ... it's due on at high noon before Class 2._

Start a new `hello-webpage` project in Glitch and make it your own. Change colors, play with formatting, play with the text. Get creative! Google around for html tips and tricks if you want. Post the link to your project in Slack in `#design-development` so we can all try it.

<a name="class2"></a>

# Class 2 • Introduction to databases

## Quick review of last week

- Some submissions 
- Fixes

### Note on "assets"

- This is where we can put images and other things
- Add an image to the assets
- Use the full url to add it to `index.html` using `<img src = "[URL OF IMAGE]" >` 
- (note image tag is one of the few in html without a closing tag. so no `</img>`.

## A different structure

### "Static"

What we did last week:

1. **Request:** You -> https://curious-scout.glitch.me -> Glitch
2. **Response:**  Glitch -> `index.html` -> you

### Static, but server-driven

 Instead of Glitch just serving up your fixed or *static* html page (as in Class 1) you're using a "server" file that serves up the page.
 
 - Search for `jkeefe` or go to [https://glitch.com/@jkeefe](https://glitch.com/@jkeefe)
 - Find `newmark-bark`
 - Remix it!
 - Name it `[yourname]-bark`

Let's take a look around ...

1. **Request:**  You -> https://newmark-bark.glitch.me -> Glitch
2. **Response:**  Glitch -> `server.js` -> `index.html` -> you

### Dynamic

1. **Request:**  You -> https://newmark-bark.glitch.me/random -> Glitch
2. **Response:**  Glitch -> `server.js` -> get data -> inject data -> `fact-page.html` -> you

## Databases!

We're going to play with a database that's probably already installed on your computer!

- Open a "Terminal" window
    - Mac: Use the "Spotlight" magnifying glass to search for Terminal
    - Windows: Use Windows Key + R (for "run') and then enter "cmd"
- Type: `mkdir mydata` <- This creates a directory called "mydata"
- Type: `cd mydata` <- This changes your directory (cd) to "mydata"
- Type: `curl -OJ "http://media.johnkeefe.net/class-modules/nyc_dogs_2012.csv"` 
- Type: `ls`, which lists the files in this directory

Let's start the database!

- Type: `sqlite3 my.db` to start SQLite and open a new database called "my.db"

"Dot" commands are special commands in SQLite that allow you to change settings and do other things.

- Type: `.mode csv`

Now we want to load our "csv" file into our database so we can run queries. Specifically, we're going to load the data from the CSV into a _table_ called "dogs" in the `my.db` database.

- Type: `.import nyc_dogs_2012.csv dogs`

If you get no response, that's a _good thing_. (Many commands just finish quietly.)

- Type: `.mode column`  <- This puts us back into column mode
- Type: `.headers on`   <- Now we'll see the column headers, too

### A little bit of SQL

SQL stands for "Sequel Query Language" and is a very powerful, if arcane, way to ask questions of a database.

The format is generally:

**SELECT** [some columns] **FROM** [a table] ... with some additional filters such as **WHERE** and **GROUP BY** and **ORDER BY** ... ended with a semicolon.

- Try `SELECT * FROM dogs;` (note the `;` at the end of a SQL command)
- Try `SELECT * FROM dogs LIMIT 10;` (note the `;` at the end of a SQL command)
- Try `SELECT dog_name, breed FROM dogs LIMIT 10;`

- Try `SELECT count() FROM dogs;`
- Try `SELECT count() FROM dogs WHERE dog_name = "Bella";`
- Try `SELECT count() FROM dogs WHERE dog_name = "bella";`
- Try `SELECT count() FROM dogs WHERE dog_name LIKE "bella";`

- Try `SELECT dog_name, count(dog_name) FROM dogs GROUP BY dog_name;`
- Try `SELECT dog_name, count(dog_name) FROM dogs GROUP BY dog_name COLLATE NOCASE;`
- Try `SELECT dog_name, count(dog_name) FROM dogs GROUP BY dog_name COLLATE NOCASE ORDER BY count(dog_name);`
- Try `SELECT dog_name, count(dog_name) FROM dogs GROUP BY dog_name COLLATE NOCASE ORDER BY count(dog_name) LIMIT 10;`
- Try `SELECT dog_name, count(dog_name) FROM dogs GROUP BY dog_name COLLATE NOCASE ORDER BY count(dog_name) DESC LIMIT 10;`

Quit SQLite3:

- Type: `.quit`



### Load the database into Glitch

- In your bark project, go to the Glitch terminal
    - Tools > Terminal
- Change directory into the `.data` directory by typing `cd .data`
- To get the CSV, type this `wget "http://media.johnkeefe.net/class-modules/nyc_dogs_2012.csv"`
- To start the database, type `sqlite3 my.db`
- To switch into CSV mode type `.mode csv`
- To import the CSV into our database, type `.import nyc_dogs_2012.csv dogs`
- Note that ^ that line created a "dogs" table within your database
- Check out if everything worked by typing: `.schema dogs`
- Switch out of csv mode: `.mode column`
- Try `SELECT count() FROM dogs WHERE dog_name LIKE "bella";`

### Dynamic with a database

1. **Request:**  You -> https://newmark-bark.glitch.me/first10 -> Glitch
2. **Response:**  Glitch -> `server.js` -> query a database -> get the answer -> turn into JSON -> you

First step, go to the `server.js` file and uncomment the SQLite code.

We'll talk about adding this code in class:

**Block one**

```javascript
app.get('/first10', function(request, response) {
  db.all('SELECT * FROM dogs LIMIT 10', function(err, rows) {
    
    if (err) {
      console.log(err)
    }
    
    response.send(JSON.stringify(rows))
  })
})
```

**Block two**

```javascript
app.get('/topnames', function(request,response) {
  db.all('SELECT dog_name, count(dog_name) FROM dogs GROUP BY dog_name ORDER BY count(dog_name) COLLATE NOCASE DESC LIMIT 10', function(err, rows) {
    
    if (err) {
      console.log(err)
    }
    
    response.send(JSON.stringify(rows))
    
  })
})
```


## Let's get some dog data

- Let's look at a [CSV of 81,000 NYC dogs](https://docs.google.com/spreadsheets/d/1dvL1vq4YTG4Y72XHlWvwTg27f1k3UVnXDZfJm5MHef8/edit?usp=sharing)


## Data on the web

- Let's look at the `index.html` file
- A little bit about JSON
- To make your life easier, download JSONview plug in

## Assignment

_This is the "Class 2" assignment. Do it now ... it's due on at high noon before Class 3._

Add a new "route" to your web service called "topbreeds" that, when hit by a web browser, returns a list of the top 5 dog breeds (by count) in the database. Submit that link in the form here.

<a name="class3"></a>

# Class 3 • Making a dynamic webpage

## Reset from last week

- Be sure to submit your attendance report
- Code live vs. video
- "topbreeds"
- Any troubles?

## Data for the web

We've been making what's known as an **API**. Officially, API stand for Application Program Interface. But I like to think of it as Another Person's Information. It's a way to get information from data on the web ... even though you usually don't actually _see_ it. It's often happening in the background.

- [How to vote in your state](https://www.washingtonpost.com/elections/2020/how-to-vote/) | Washington Post
- [Nursing home inspect](https://projects.propublica.org/nursing-homes/) | ProPublica
- [The NYPD files](https://projects.propublica.org/nypd-ccrb/) | ProPublica
- [Tracking Covid at US Colleges](https://www.nytimes.com/interactive/2020/us/covid-college-cases-tracker.html) | New York Times
- [The Weather](https://www.weather.gov/) | Weather.gov
- [Pollen Counts](https://www.aaaai.org/global/nab-pollen-counts) | AAAAI

Let's make an API specifically for providing data on how many dogs are named ... whatever name we're asked ... and then make it easy to use.

- It will [look like this](https://newmark-bark.glitch.me/form) when it's done!

## Code walk-through

<iframe src="https://player.vimeo.com/video/456422529?title=0&byline=0&portrait=0" width="640" height="400" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
<p><a href="https://vimeo.com/456422529">Design &amp; Development - 03 Walkthrough</a> from <a href="https://vimeo.com/jkeefe">John Keefe</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

The code walk-through is embeded above and also [posted on Vimeo](https://vimeo.com/456422529) so you can go at your own pace — pause, speed up, go back. (Note that, oddly, the speed controls are only available on the embedded version above; they don't show up on the Vimeo site.)

## Quick SQL review

Remember, we used SQL to query the database for information.

The syntax, again, is: `SELECT [columns or pseudo-columns] FROM [table] ... [more options]`

- `SELECT dog_name, breed FROM dogs LIMIT 10;`
- `SELECT count() FROM dogs;`
- `SELECT count() FROM dogs WHERE dog_name LIKE "bella";`
- `SELECT dog_name, count() as total FROM dogs WHERE dog_name LIKE "bella";`

Also remember we can put these queries into our "server.js" file on Glitch.

## Making a lookup form on our site

We're going to provide a _service_ to our audience by making it super easy for them to find out how many dogs are named like theirs.

**Block 3**

```javascript
app.get('/name/max', function(request,response) {
  db.all(`SELECT dog_name, count(dog_name) AS total FROM dogs WHERE dog_name LIKE "max"`, function(err, rows) {
    
    if (err) {
      console.log(err)
    }
    
    response.send(JSON.stringify(rows))
    
  })
})
```

- note that we're changing "max" to a variable called `:input` ... and then using that in the SQL query as `${request.params.input}`.

**Block 3A**

```javascript
app.get('/name/:input', function(request,response) {
  db.all(`SELECT dog_name, count(dog_name) AS total FROM dogs WHERE dog_name LIKE "${request.params.input}"`, function(err, rows) {
    
    if (err) {
      console.log(err)
    }
    
    response.send(JSON.stringify(rows))
    
  })
})
```

Let's build a lookup form!

- In the left-hand column, find `/views` and click on the three little dots.
- Pick "Add file to Folder"
- Call it `form.html`
- Click on that new file, `form.html`
- Into the big blank box in the middle of the screen, paste Block 4:


**Block 4**

```html
<!DOCTYPE html>
<html>
<body>
    
    <form>
        What's your dog's name?<br>
        <input type="text" id="dog_box" onkeyup="hitAPI()"><br>
    </form>
    <div id="answer_line"></div>

    <script>
        function hitAPI() {
          
            var input_name = document.getElementById("dog_box").value
            var xhttp = new XMLHttpRequest()
            
            xhttp.onreadystatechange = function() {
                if (this.readyState == 4 && this.status == 200) {
                    data = JSON.parse(this.responseText)
                  document.getElementById("answer_line").innerHTML = `There are ${data[0].total} dogs named ${input_name} in NYC.`
                }
            }
                
            if (input_name != "") {
              xhttp.open("GET", `/name/${input_name}`, true)
              xhttp.send()
            } else {
              document.getElementById("answer_line").innerHTML = ""
            }
                    
        }
    </script>
</body>
</html>
```

Now we need a _route_ to our form.

**Block 5**

In your `server.js` file, add this route. For organization's sake, put it right after the first route ... the one that sends people to `index.html`.

```javascript
app.get('/form', function(request, response) {
  response.sendFile(__dirname + '/views/form.html');
});
```


## Assignment

_This is the "Class 03" assignment. Do it now ... it's due on at high noon before Class 04._

Complete the steps above so that your form _works_ and answers the question for any name I enter. Paste the _Show_ URL into the form below and submit it by the deadline. The URL should be like `my-bark-site.glitch.me/form`.

_If you get stuck_ try backing up and following my steps again. If you still can't get it to work, you have options:

1. Go to the `#design-development` channel in the social-j Slack and post the "edit" link to your code. That link will begin like this: `https://glitch.com/edit/#!/your-project ...`. Include a short description of what's not working and what you've already tried. 
2. Join my "helpdesk hours" Wednesday at 12:30 pm. The link for that has been added to the syllabus and will be posted in the `#design-development` chat every Wednesday morning.

<a name="class4"></a>

# Class 4 • Introduction to conversational interfaces

Automatically processing what someone is saying -- either in a chat, to a voice assistant, or in an email -- is increasingly possible thanks to machine learning. We'll play with one of these natural language processing tools (such as Dialogflow) to get a handle on how to make it work for you.

## Utterances

These are things humans might say or type to a bot. 

- How much is a plane ticket to Miami?
- Where's the nearest dog park?
- What's the weather going to be like tomorrow?
- Yes, I agree.
- Nope.
- I'm in New York.
- Wow!

When building a bot, you need to have a _sense_ of what kinds of things your users might ask — so it helps to declare up front what kinds of things it can answer!

_Hi! I'm the Newmark Bark Bot and I can answer questions about dogs and dog ownership in New York City_.

Utterances are used to train the bot, and in Dialogflow these called "Training Phrases."

## Intents

Intents are categories of questions we can answer, and usually track with some basic function the human is asking the bot to do. Many utterances can lead to the same intent:

- How much is a plane ticket to Miami?
- What does it cost to fly from New York to London?
- What's the price of a plane trip from Chicago to Los Angeles?

What's the intent here? We might say it's `air-travel-price`.

But intents can be simpler than that, too. 

- Yes!
- Yup.
- You bet!
- Si.
- Of course

... all mean "yes" to the bot. So we could group these into an intent called `response-yes`.

And these:

- No way
- Nope
- nada
- no
- Heck no

... all mean "no" to the bot. So we could group these into an intent called `response-no`.

And for our exclamations,

- Wow
- OMG
- whoa!
- I can't believe it!
- Amazing

And words like these could mean the `response-wow` intent.

So you could make bot responses to those _intents_ instead of those words, and let the Natural Language Processor decide which intent is, um, intended.

## Entities

Consider our `air-travel-price` intent from above:

- How much is a plane ticket to Miami?
- What does it cost to fly from New York to London?
- What's the price of a plane trip from Chicago to Los Angeles?

While the _intent_ may be the same ("tell me the price of a plane trip"), the answers are definitely not going to be the same, right?

In order to formulate an answer, we'd need some information:

- Where are you flying from?
- Where are you flying to?
- When?
- What airline?
- What class of seat?

The portions of the intent you need to answer a specific question are called "entities" (and also "slots" and "elements" and probably many other things, sorry!) 

Entities here would include "Miami," "New York," "Chicago," and really any moderately sized city. They'd also include "Delta," "American," "JetBlue," and really any airline. Also "September 18, 2020" and "8 pm" and any other date/time combination. These are all "Entities."

### Another example

Consider the following phrases:

- What's the forecast in Minneapolis tomorrow?
- Will it rain in New York Friday?
- What's the temperature outside?
- Do I need an umbrella?

You might call this a `get-forecast` intent. To answer a "forecast" intent, you need two additional pieces of information: Where and when. Entities!

So a `get-forcast` intent requires `place` and `time`.

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
    
We can set up our bot so that if the entity is missing, the bot asks for it. 

## Contexts

Context is information about where we are (or, more often, where we just were) in the conversation. Context becomes important when the same response has different meanings in different parts of the conversation.

For example, "yes" means something different if the question is "Do you like cats?" instead of "Do you like dogs?"

I like to think of "Contexts" as breadcrumbs we can leave along the way to keep track of the conversation.

## Training

To train a bot — really a machine-learning _model_ — we do the following:

1. Set up an intent.

2. Come up with as many training phrases as possible to trigger that intent. The more the better! Usually you'll want at least 10.

3. Write a response to that intent, which could be another question.

Interestingly, most natural language systems allow you to review its decisions and _train_ it when it performed well and performed poorly.


## Introduction to Dialogflow

There are lots of tools out there to use to make bots. We'll play with [Dialogflow](https://dialogflow.cloud.google.com).

Follow the instructions in this week's coding walk-through video:

<iframe src="https://player.vimeo.com/video/457600740" width="640" height="400" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>

You can also see the video [on the Vimeo site](https://vimeo.com/457600740).

### Setup

You'll need to be logged into your J-School account or any Google/Gmail account.

- Go to [Dialogflow](https://dialogflow.cloud.google.com)
- Choose "Create Agent" -- and you may need to authenticate with Google again here.
- Note that you can think of "Agents" as one bot brain. What you teach one agent isn't (easily) shared with another agent.
- Name it "DogBot" (no spaces allowed)
- Leave the rest of the page as it is.
- Click "Save"

OK, your "agent" is established.

- If you don't see a sidebar on the left side, click the menu icon (the three horizontal lines)

### Building a dog bot

Elaboration for all of these steps is in this week's [walk-through video](https://vimeo.com/457600740).

- Establish the welcome intent.
    - "Hello! I'm here to help NYC dogs and their owners. You can play the pet quiz, find a dog run, or look up your dog's name. What would you like to do?"
- Build the each intent.
    - Come up with 5 phrases
    - Include a response text
    - Test them out
- Build the Pet Quiz
- What happens if you say something wrong?
    - That's the "Fallback intent" ... let's fix that.
- Share it with the world (and your instructor):
    - Go to integrations
    - Flip the switch on "Web demo"
    - Copy the link to the bot
    - NOTE! I forgot to mention this, but you can also get an EMBED code here to put the bot on your own site.
- Fill out the assignment form, including that URL

## Assignment

_Check out Google Classroom for the "04 Assignment." You'll need the URL from the end of the video.  Do it now ... it's due on at high noon on the day of our next class._

_If you get stuck_ try backing up and following my steps again. If you still can't get it to work, you have options:

1. Go to the `#design-development` channel and provide a short description of what's not working and what you've already tried. 
2. Join my "helpdesk hours" Wednesday at 12:30 pm. The link for that has been added to the syllabus and will be posted in the `#design-development` chat every Wednesday morning.

<a name="class5"></a>

## Class 5 • Talk to me: Making a voice service for Google Home

## Let's make it!

### Video walk-through

<iframe src="https://player.vimeo.com/video/461499760?title=0&byline=0&portrait=0" width="640" height="400" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
<p><a href="https://vimeo.com/461499760">Design &amp; Development: Class 5 Walk-through</a> from <a href="https://vimeo.com/jkeefe">John Keefe</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

#### Update our Glitch app to get ready for requests from Dialogflow

[Make a little drawing]

- Log into Glitch
- We need to make a new route. It's like the "form," but it's specific to Dialogflow, so we can accept Dialogflow's request and make an answer. Here's the code:

**Block 6**

```javascript
app.post('/dialogflow', function(request, response){
  
  var search_dog = request.body.queryResult.queryText
  
  db.all('SELECT dog_name, count(dog_name) AS total FROM dogs WHERE dog_name LIKE "' + search_dog + '" GROUP BY dog_name COLLATE NOCASE', function(err, rows) {
    
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
#### Tell Dialogflow where to get the answers

- Log into Dialogflow
- First we're going to let Dialogflow that we're going to use a "Fulfillment" service (our Glitch site!) to help answer questions. Click on the "Fulfillment" tab.
- Here, flip the webhook switch from "Disabled" to "Enabled" at the top so it's blue.
- We need to provide our dog service's URL. It'll be in this format: `https://[your-project-name].glitch.me/dialogflow`
- Put that into the Dialogflow webhook "URL" line (don't forget the `/dialogflow` at the end!)


#### Set up the conversation

- Go to the "DogNameLookup" intent 
- Change the output text to "Excellent! What's your dog's name?"
- Also need to add an Output Context! Let's call it `asked-for-name`
- Need to make a new intent. But this is a **fallback intent**. That is, we're not trying to detect what they say from the language. We want the answer, no matter _what_ the human says. But we also don't want to go to the **default fallback intent** . That's why we set the output context. So if we're waiting for a response to `asked-for-name` we'll use this. There's a special place to make these intents.
- Let's call it `CheckGlitchForName`
- Add an "Input Context": `asked-for-name` (give it a duration of 1)
- Open the "Fulfillment" section (in the main part of the window)
- Turn on the switch for "Enable webhook call for this intent."
- Give it a try in the test window.
- Give it a try in the web chat
- Once the DogNameLookup works on the web chat, submit this link (just like last week).

#### Do it with your voice!

- Go to "Integrations"
- Pick Google Assistant
- Click "TEST" at the bottom.
- Wait for it to get set up "Actions on Google" (takes a full minute or so)
- Allow location use
- Click on the microphone
- Allow microphone use
- Say "Talk to my test app"
- Answer the questions! (**You have to click the microphone before you say something**)
- Fun!

<a name="class6"></a>

## Class 6 • Getting & giving insights with forms

- Making a form in Google Forms
- Making a form in Typeform
- Making a form in Airtable

### Walk-through video

<iframe src="https://player.vimeo.com/video/464007934?title=0&byline=0&portrait=0" width="640" height="400" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
<p><a href="https://vimeo.com/464007934">Design &amp; Development 06 Walk-through</a> from <a href="https://vimeo.com/jkeefe">John Keefe</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

### Airtable "Base"

- Head over to [airtable.com](https://airtable.com).
- Start a new "base"
- Then make a few entries
- Delete any blank entries

### Check out its custom API

- Then head over to the api section at [api.airtable.com](https://airtable.com/api)
- Pick the same "base" you made in the last step. This will get you to the API info for that base.

### Get your API key

- We need to establish an API key that is your secret code to accessing your API.
- Scroll down to the "Authentication" section section and click on the word "account" where the text says "visit your account page." (You can also just go to https://airtable.com/account)
- Generate an API key on this page.

### See it in action

- Head back to the "Airtable API" page (the one with the light and dark columns)
- Click "show api key" at the top right
- Then copy the url (not the `curl` part) from under "Example Using Query Parameter"
- Open a new tab in your browser and paste that in to see your story data on the internet.

### Put your API key in Glitch

- Again, head back to the "Airtable API" page (the one with the light and dark columns)
- Back on the Airtable API tab, click "JavaScript" at the top of the darker column. This will switch the code in that column to JavaScript, which is what we need.
- Look for the line that looks like this: 

```
$ export AIRTABLE_API_KEY=keyVblahBLAHblah
```

- Copy all of the letters to the right of the equals sign `=` (including the lower-case "key" at the beginning of those letters)
- Now open new tab and go to https://glitch.com 
- Open view your "bark" project
- Go to the `.env` file
- Paste the API key in the box where it goes

### Get the identity of your base

- Go back to the Airtable API tab
- Find the line that looks like this:

```javascript
const base = require('airtable').base('appuKFpVClZjDsvUm');
```
- Copy it (but not mine here in these notes ... copy it from _your_ Airtable)
- Go back to Glitch, and pick the `server.js` file
- Paste that line of code in `server.js` right above the line that says `/// URL ROUTES BELOW ...`

### Build a "dog news" page

- In Glitch make a new file in the `views` folder
- Name it `news.html`
- Paste Block 7 into this file

**Block 7**

[View Block 7 code here](https://gist.github.com/jkeefe/220a57606bb6ebd9b75d4e4f65679bad).

- Open a little space just above the line that says `// listen for requests`
- We're going to add a new "route" called `/news`. Copy and paste Block 8 into this spot:

**Block 8**

```JavaScript
app.get('/news', function(req, resp) {
  
  // let's set up the data with a spot for stories
  var data = {'stories':[]}
  
  // NOTE! If your page isn't updating, try increasing
  // this number by one. Just changing it makes the
  // news.html page refresh
  data.cachebust = 2
  
  // go hit out Airtable!
  base('Table 1').select({
    view: 'Grid view'
  }).firstPage(function(err, records) {
    
      // log an error if something breaks
      if (err) { console.error(err); return; }
    
      // loop through the items and 
      // add them to "data" (using Airtable's code)
      records.forEach(function(record) {
          data.stories.push({
            "Name": record.get('Name'),
            "Notes": record.get('Notes')
          })
        
      })
    
      console.log(data)
    
      // pass the data to the html template and serve up the page
      resp.render('news.html', data)
    
  })
  
})
```

- View your news at your projet url `/news`
- Paste that URL into the homework!

<a name="class7"></a>

## Class 7 • Chatbots for collecting information in real time

## Video walk-through

<iframe src="https://player.vimeo.com/video/466304040?title=0&byline=0&portrait=0" width="640" height="400" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
<p><a href="https://vimeo.com/466304040">Design &amp; Development Walkthrough: Class 7</a> from <a href="https://vimeo.com/jkeefe">John Keefe</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

## Code you'll need

**Block 9**

```javascript
base('Table 2').create([
  {
    "fields": {
      "Name": search_dog
    }
  }
], function(err, records) {
  if (err) {
    console.error(err);
    return;
  }
});
```

## Assignment

Complete the video tasks and paste your Glitch project url in the assignment form.


<a name="class8"></a>

## Class 8 • Identifying and communicating your hopes and dreams


## Assignment

Use the project communication document for a project of yours (or your imagination) assigned in Google Classroom.

<a name="class9"></a>

## Class 9 • Make bots to do your bidding

We did a review of IFTTT, Zapier, Google Alerts, and Klaxon to help you monitor the internet and collect data.

## Assignment

1. Create a new applet/bot using IFTTT (at https://ifttt.com)
2. Go to the applet's "settings"
3. Take a screenshot of the area where I can see both the trigger and the action (so mainly the area below the "Check now" button)
4. Submit that screenshot using the Google Classroom assignment page.

<a name="class10"></a>

## Class 10 • APIs, scraping and other data sources

### Digging before scraping

- Sometimes the data is there in a json file or via an api, under the hood.

### Scraping Example 1

Drawn from a [Medium post by Julia Kho](https://towardsdatascience.com/how-to-web-scrape-with-python-in-4-minutes-bc49186a8460).

Python notebook on Google Colab.

### More exploration

- [Great walk-through](https://www.dataquest.io/blog/web-scraping-tutorial-python/), using the weather service as an example.

<a name="class11"></a>
<a name="class12"></a>
<a name="class13"></a>
<a name="class14"></a>

------

_Notes for subsequent classes will be posted prior to the class itself._


