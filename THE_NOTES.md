 [The Syllabus](./README.md) | [The Notes](./THE_NOTES.html)

# The Notes

Here's where you'll find resources, code, links, and notes for every class. Materials are added here generally at least one day before each class, but can change and get updated up until class time.

<a name="class1"></a>

# Class 1 • Basic internetting

## Introductions

- A bit about me
    - [Personal website](https://johnkeefe.net)
    - [CNN](https://cnn.com/)
    - Twitter: [@jkeefe](https://twitter.com/jkeefe)
    - Email: john.keefe (at) journalism.cuny.edu
    - Slack is better! [Here's our Slack](https://socialjournalism2021.slack.com).
    
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
- Everyone in the Slack! [Join here](https://socialjournalism2022.slack.com) and use your school email address. Join channel **#design-development**.

## Exploring web pages

- Sign up for [Glitch](https://glitch.com)
- Make a new project > `glitch-hello-webpage`
    - Data journalism classes: Started from scratch & uploaded to Github
    - Glitch: Start from something that already works
    - Basic layout of the page
        - Name button
            - Change the theme if you'd like
        - The files
        - A file
        - The result (which has its own URL ... which I'll call the "live site" url)
        - The share button
    - Go through `index.html`
    - Note the other files
    - Back to `README.md`
    - Click on the link where it says:
    
    ```
    Want a minimal version of this project to build your own website? Check out Blank Website!
    ```

- Much closer to blank! Just the essentials.
- Take a close look at all the files. Make sure you understand what's happening here.
- Remember that the public url first looks at `index.html`

## Assignment

_This is the "Class 1" assignment. Do it now ... it's due on at high noon before Class 2._

 Continue to play with this project in Glitch and make it your own. Change colors, play with formatting, play with the text. Get creative! Google around for html tips and tricks if you want. Post the **live link** to your project in Slack in `#design-development` so we can all try it.

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

### "Dynamic"

1. **Request:**  You -> https://newmark-bark.glitch.me -> Glitch
2. **Response:**  Glitch -> `server.js` -> `index.html` -> you

Instead of Glitch just serving up your fixed or *static* html page (as in Class 1) you're using a "server" file that serves up the page.
 
 - Search for `jkeefe` or go to [https://glitch.com/@jkeefe](https://glitch.com/@jkeefe)
 - Find `newmark-bark`
 - Remix it!
 - Name it `[yourname]-bark`

Let's take a look around ... 

See how the main page, `index.html`, is served.

We can also make a new "about" page by adding a new _view_ page and a new _route_.

Here's the view page, which we'll call `views/about.html`:

```html
<html>
  
  <head>
    <title>About Us</title>
  </head>
  
  <body>
      
    <h1>
      About Newmark Bark
    </h1>
    
    <p>
      Newmark Bark is a service of the Newmark Graduate School of Journalism at CUNY.
   </p>
   
  </body>
  
</html>
```

Here's the route, which goes in the `server.js` file under the line that says put the routes under this line!

```js
// this is the "home" page or the regular url

app.get('/about', function(request, response) {
  response.sendFile(__dirname + '/views/about.html');
});
```

(can also add the stylesheet to the `about.html` page by putting this code inside the `<head>` tags):

```html
<!-- import the webpage's stylesheet -->
<link rel="stylesheet" href="/style.css">
```

### Why all the hassle?

Here's why ... with a "dynamic" page, we can alter the page before sending it back to the user.

For example, try visiting: https://newmark-bark.glitch.me/random (note the "random" at the end!)

1. **Request:**  You -> https://newmark-bark.glitch.me/random -> Glitch
2. **Response:**  Glitch -> `server.js` -> get data -> inject data -> `fact-page.html` -> you

We can _inject_ the page with data before serving it up.

But what if you have more than 6 rows of data?

## Databases!

We're going to play with a database that's already up an running online.

- Go to: https://datasette.johnkeefe.net/
- Click on "nyc_dog_licenses" (It's below "fundata")
- Take a look around! 👀
    - Be sure you understand the data, what's here, what's not
- Click on "view and edit SQL"
- Clear out the box that's there. We're going to start from scratch.

### A little bit of SQL

SQL stands for "Sequel Query Language" and is a very powerful, if arcane, way to ask questions of a database.

The format is generally:

- **SELECT** [the columns you want to see] **FROM** [a table]
- ... with additional filters such as **WHERE** and **GROUP BY** and **ORDER BY**

#### SELECT

- Try `SELECT * FROM nyc_dog_licenses;` and click "Run SQL" (note the `;` at the end of a SQL command is often required, though we don't need it on this website)
- Try `SELECT * FROM nyc_dog_licenses LIMIT 10;`
- Try `SELECT AnimalName, BreedName FROM nyc_dog_licenses LIMIT 10;`

#### count() & WHERE

- Try `SELECT count() FROM nyc_dog_licenses;`
- Try `SELECT count() FROM nyc_dog_licenses WHERE AnimalName = "BELLA";`
- Try `SELECT count() FROM nyc_dog_licenses WHERE AnimalName = "Bella";`
- Try `SELECT count() FROM nyc_dog_licenses WHERE AnimalName LIKE "bella";`

#### GROUP BY & ORDER BY

- Try `SELECT AnimalName, count(AnimalName) FROM nyc_dog_licenses GROUP BY AnimalName;`
- Try `SELECT AnimalName, count(AnimalName) FROM nyc_dog_licenses GROUP BY AnimalName ORDER BY count(AnimalName);`
- Try `SELECT AnimalName, count(AnimalName) FROM nyc_dog_licenses GROUP BY AnimalName ORDER BY count(AnimalName) DESC;`
- Try `SELECT AnimalName, count(AnimalName) FROM nyc_dog_licenses GROUP BY AnimalName ORDER BY count(AnimalName) DESC LIMIT 10;`


#### AS

- Try `SELECT AnimalName, count(AnimalName) AS TotalDogs FROM nyc_dog_licenses GROUP BY AnimalName ORDER BY TotalDogs DESC;`

### Break!

### Load the database into your Glitch project

1. In your bark project, go to the Glitch terminal
    - Tools > Terminal
1. Type: `cd .data` to **c**hange **d**irectory to the `.data` directory
1. Copy-paste this and hit return:
```
wget "http://s3.amazonaws.com/media.johnkeefe.net/data/NYC_Dog_Licensing_Dataset_2018.csv"
sqlite3 my.db '.mode csv' '.import NYC_Dog_Licensing_Dataset_2018.csv nyc_dog_licenses'
```
1. Type: `sqlite3 my.db` to start the database
1. Type:  `SELECT count() FROM nyc_dog_licenses;` to test it!
1. Can even do: `SELECT AnimalName, count(AnimalName) FROM nyc_dog_licenses GROUP BY AnimalName ORDER BY count(AnimalName) DESC LIMIT 10;`
1. Type: `.exit` to exit
1. Close the Terminal with the "X" at the right

### Dynamic with a database

1. **Request:**  You -> https://newmark-bark.glitch.me/first10 -> Glitch
2. **Response:**  Glitch -> `server.js` -> query a database -> get the answer -> turn into JSON -> you

#### Let'a make it!

First ...
- In Glitch go to the `server.js` file 
- Uncomment the SQLite code.
    - That means delete the `//` from the beginning of the lines
    - (But not all of those on the first one, which is just a label)
    - A shortcut: highlight the lines and press `[command] /``

We'll talk about adding this code in class:

**Block one**

```javascript
// watch for "first10" in the URL
app.get('/first10', (request, response) => {
    
    // set the query
    let query = 'SELECT * FROM nyc_dog_licenses LIMIT 10'
  
    // run the query
    db.all(query, (err, rows) => {
    
        // let us know if something went wrong
        if (err) {
          console.log(err)
        }
    
        // otherwise, send a "response" with a JSON version of the rows we got
        response.send(JSON.stringify(rows))
  })
  
})
```

## We're seeing data on the web

- A little bit about JSON
- To make your life easier, download JSONview plug in


**Block two**

```javascript
// watch for "toppnames" in the URL
app.get('/topnames', (request,response) => {
    
    // set the query
    let query = 'SELECT AnimalName, count(AnimalName) as TotalDogs FROM nyc_dog_licenses GROUP BY AnimalName ORDER BY TotalDogs DESC LIMIT 10'
  
    // let us know if something went wrong
    db.all(query, (err, rows) => {

        // let us know if something went wrong
        if (err) {
          console.log(err)
        }

        // otherwise, send a "response" with a JSON version of the rows we got
        response.send(JSON.stringify(rows))

    })
})
```

## Assignment

_This is the "Class 2" assignment. Do it now ... it's due on at high noon before Class 3._

Add a new "route" to your web service called "topbreeds" that, when hit by a web browser, returns a list of the top FIVE dog breeds (by count) in the database.

Submit that "topbreeds" live link in the Google Classroom assignment form. That link will look like `https://https://newmark-bark.glitch.me/topbreeds` ... but with your name instead of `newmark`.

Remember that your can find your base "live link" by clicking the "Share" button. 

<a name="class3"></a>

# Class 3 • Making a dynamic webpage

## Reset from last week

- Be sure to submit your attendance report
- Code live vs. video
- "topbreeds"
- Any troubles?

## Data for the web

We've been making what's known as an **API**. Officially, API stand for Application Program Interface. But I like to think of it as Another Person's Information. It's a way to get information from data on the web ... even though you usually don't actually _see_ it. It's often happening in the background.

- [The Weather](https://www.weather.gov/) | Weather.gov
- [How to vote in your state](https://www.washingtonpost.com/elections/2020/how-to-vote/) | Washington Post
- [Nursing home inspect](https://projects.propublica.org/nursing-homes/) | ProPublica
- [The NYPD files](https://projects.propublica.org/nypd-ccrb/) | ProPublica
- [Tracking Covid at US Colleges](https://www.nytimes.com/interactive/2020/us/covid-college-cases-tracker.html) | New York Times

Let's make an a service specifically for providing data on how many dogs are named ... whatever name we're asked ... and then make it easy to use.

- It will [look like this](https://newmark-bark.glitch.me/form) when it's done!

## Code walk-through

<iframe src="https://player.vimeo.com/video/456422529?title=0&byline=0&portrait=0" width="640" height="400" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
<p><a href="https://vimeo.com/456422529">Design &amp; Development - 03 Walkthrough</a> from <a href="https://vimeo.com/jkeefe">John Keefe</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

The code walk-through is embeded above and also [posted on Vimeo](https://vimeo.com/456422529) so you can go at your own pace — pause, speed up, go back. (Note that, oddly, the speed controls are only available on the embedded version above; they don't show up on the Vimeo site.)

## Quick SQL review

Remember, we used SQL to query the database for information.

The syntax, again, is: `SELECT [columns or pseudo-columns] FROM [table] ... [more options]`

- `SELECT AnimalName, breed FROM dogs LIMIT 10;`
- `SELECT count() FROM dogs;`
- `SELECT count() FROM nyc_dog_licenses WHERE AnimalName LIKE "bella";`
- `SELECT AnimalName, count() as total FROM nyc_dog_licenses WHERE AnimalName LIKE "bella";`

Also remember we can put these queries into our "server.js" file on Glitch.

## Making a lookup form on our site

We're going to provide a _service_ to our audience by making it super easy for them to find out how many dogs are named like theirs.

**Block 3**

```javascript
app.get('/name/max', function(request,response) {
  db.all(`SELECT AnimalName, count(AnimalName) AS total FROM nyc_dog_licenses WHERE AnimalName LIKE "max"`, function(err, rows) {
    
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
  db.all(`SELECT AnimalName, count(AnimalName) AS total FROM nyc_dog_licenses WHERE AnimalName LIKE "${request.params.input}"`, function(err, rows) {
    
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

Complete the steps above so that your form _works_ and answers the question for any name I enter. Paste the _Show_ URL into the form below and submit it by the deadline. The URL should be like `name-bark.glitch.me/form`.

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
<a name="class6"></a>
<a name="class7"></a>
<a name="class8"></a>
<a name="class9"></a>
<a name="class10"></a>
<a name="class11"></a>
<a name="class12"></a>
<a name="class13"></a>
<a name="class14"></a>
<a name="class15"></a>

------

_Notes for subsequent classes will be posted prior to the class itself._


