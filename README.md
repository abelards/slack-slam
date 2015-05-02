# slack-slam

A key-value store for Slack

### Setup

#### Install app
Clone this repo to your computer and deploy it as you would a Rails app.

If you're using Heroku, Scalingo or such, change `config/database.yml`
to uncomment the lines with `DATABASE_URL` and comment the other `production:` vars.
Set your own `SECRET_KEY_BASE`.

#### Authorising
In your Slack app, use the menu to find the integrations panel: `https://YOUR_TEAM.slack.com/services/new`.

Search for **Outgoing webhook** and add it. Scroll down to **Integrations settings** to choose channel (optional), trigger word, and point the URL to your app `/message` route (example below).
![Imgur](http://i.imgur.com/wlQILQC.png)

Use Slack's page to [register your application](https://api.slack.com/applications) and get your
`SLACK_CLIENT_ID` and `SLACK_CLIENT_SECRET`.
Then, just visit [slack-slam.herokuapp.com](http://slack-slam.herokuapp.com) and authorize yourself.

#### Seeding the DB
You then need to populate the DB with the team and users, so go to the Slack API doc on `users.list` and `team.info` and try the "Test" tab to get info in a convenient Web form:
https://api.slack.com/methods/users.list/test
https://api.slack.com/methods/team.info/test

Then run a console and seed the database:
```
t = Team.create(slack_team_name: 'team', slack_team_id: '42')
u = User.create(slack_name: 'me', slack_user_id: '42', t.id, access_token: 'xxx')
```

### Usage
Basic Commands
```
slam help # shows your user info
slam add <key> <value> # assign a new value to a key
slam <key> # references a key
slam list # lists all your key-value pairs
slam save <key> # saves either the last posted .gif or the last message a user other than yourself
```

Bonus stuff
```
slam weather <city> # weather for a specific city
slam trivia # a random trivia question
slam trivia-ans # answers to the last trivia question in the channel
slam yoda <phrase> # converts the phrase to yoda speak
slam joke # a random chuck norris joke
slam quote # a random movie quote
```

Example usage
```
# assign the key 'uwaterloo' the value 'is an awesome university'
slam add uwaterloo is an awesome university

# reference a previously stored key
slam uwaterloo #=> is an awesome university
```

### Contributors
* [Angel Gao](https://github.com/angelgao)
* [Jason Loo](https://github.com/nosajool)
* [Matthew Du](https://github.com/matthewdu)
