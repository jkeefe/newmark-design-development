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

## A little more advanced Internetting

- Search for `jkeefe` or go to [https://glitch.com/@jkeefe](https://glitch.com/@jkeefe)
- Find `newmark-bark-2020`
- Remix it!
- Name it `[yourname]-bark`

## A different structure

### "Static"

What we did last week:

1. **Request:** You -> https://curious-scout.glitch.me -> Glitch
2. **Response:**  Glitch -> `index.html` -> you

### Static, but server-driven

 Instead of Glitch just serving up your fixed or *static* html page (as in Class 1) you're using a "server" file that serves up the page.
 
- Go to Glitch
- Use the search function to find my projects `jkeefe`
- Find the "Newmark-Bark" project and "Remix" it

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
<a name="class4"></a>
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

------

_Notes for subsequent classes will be posted prior to the class itself._


