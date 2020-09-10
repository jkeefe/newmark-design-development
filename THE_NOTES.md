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


