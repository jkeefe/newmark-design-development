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
- To get the CSV, type this `wget -P "http://media.johnkeefe.net/class-modules/nyc_dogs_2012.csv"`
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
    - **Request** Your phone > the service phone number > Twilio > Our Glitch site
    - **Response** Our Glitch site > Twilio > your phone number > your phone 
        
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

_This is the "Class 2" assignment. Do it now ... it's due on at high noon before Class 4 (Which is THURSDAY)._

Add a the new "route" to your web service that so that when I text your phone number I get the right number of dogs. Make sure it works and post a screenshot of your interaction with your bot into Slack.




