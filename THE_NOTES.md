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

## A little more advanced Internetting

- Search for `jkeefe` or go to [https://glitch.com/@jkeefe](https://glitch.com/@jkeefe)
- Find `newmark-bark-data`
- Remix it!
- Name it `[yourname]-bark-data`

## A different struture

- Instead of Glitch just serving up your fixed or *static* html page (as in Class 1) you're running a "server" file that serves up the page.
- Let's walk through how `index.html` gets served in this case
- Focus only on the `app.get('/',` section for now

### Understanding "assets"

- This is where we can put images and other things
- Add an image to the assets
- Use the full url to add it to `index.html`

## Let's get some dog data

- Let's look at a [CSV of 81,000 NYC dogs](https://docs.google.com/spreadsheets/d/1dvL1vq4YTG4Y72XHlWvwTg27f1k3UVnXDZfJm5MHef8/edit?usp=sharing)
- 


## Databases!

- Go to the Glitch console
- Change directory into the `.data` directory with `cd .data`
- To get the CSV, type this `wget -P "http://media.johnkeefe.net/class-modules/nyc_dogs_2012.csv"`
- To start the database, type `sqlite3 dogs.db`
- To switch into CSV mode type `.mode csv`
- To import the CSV into our database, type `.import nyc_dogs_2012.csv doginfo`
- Note that ^ that line created a "doginfo" table within our database
- Check out if everything worked by typing: `.schema doginfo`
- Try `SELECT * FROM doginfo LIMIT 10;`
- Try `SELECT dog_name, count(dog_name) FROM doginfo GROUP BY dog_name;`
- Try `SELECT dog_name, count(dog_name) FROM doginfo GROUP BY dog_name COLLATE NOCASE;`
- Try `SELECT dog_name, count(dog_name) FROM doginfo GROUP BY dog_name COLLATE NOCASE ORDER BY count(dog_name);`
- Try `SELECT dog_name, count(dog_name) FROM doginfo GROUP BY dog_name COLLATE NOCASE ORDER BY count(dog_name) DESC LIMIT 10;`
- Try `SELECT dog_name, count(dog_name) FROM doginfo WHERE dog_name LIKE "max" GROUP BY dog_name COLLATE NOCASE`

## Data on the web

- Let's look at the `index.html` file
- A little bit about JSON
- To make your life easier, download JSONview plug in

## Assignment

_This is the "Class 2" assignment. Do it now ... it's due on at high noon before Class 3._

Add a new "route" to your web service that, when hit by a web browser, displays a list of the top 5 dog breeds (by count) in the database. Paste a link to that route into Slack.








