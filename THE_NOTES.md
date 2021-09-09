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
<a name="class15"></a>

------

_Notes for subsequent classes will be posted prior to the class itself._


