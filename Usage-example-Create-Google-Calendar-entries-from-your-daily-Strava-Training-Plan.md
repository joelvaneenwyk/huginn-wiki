This usage example was written by @Chaosspeeder.

### New Year Resolutions: Participate at a marathon and automate my life.

Ok, this sound silly and maybe it is, but I want to use my (poor) coding skills to automate things as far as possible and I also want to participate at a marathon this year. Oh and by the way, I am not the youngest person on earth anymore :-)

For preparation for my marathon I started a training plan on [Strava](https://www.strava.com), a platform for fitness enthusiasts. Strava send me a daily instruction for my training via email. But I want the instructions as a google calendar entry, where I organize all things through a day. So I started dealing with _Huginn_, to gain experience in automating things.

I created in Huginn a workflow like this:

![My workflow](https://farm2.staticflickr.com/1551/24360536849_bf3d68b7e7_o.png)

And combined the needed agents in one scenario:

![Training Plan as scenario](https://farm2.staticflickr.com/1569/24101494863_a87afba574_o.png)

### Step 01: Check regularly my Gmail account for a new training plan.

I use the IMAP Folder agent to check gmail several times a day for a new mail from Strava:

````
{
  "expected_update_period_in_days": "1",
  "host": "imap.gmail.com",
  "ssl": true,
  "username": "{% credential google_username %}",
  "password": "{% credential google_password %}",
  "folders": [
    "INBOX"
  ],
  "conditions": {
    "subject": "Strava Trainingsplan - Woche \\d+ Tag \\d+"
  }
}

This agent generates an event payload with the important data of the fetched mail: subject and body.

````

### Step 02 - Extract the information out of the body and create a google calendar message

Now the things become somewhat nasty. The needed information about the training is buried in the body of the mail. I have to extract the information via regular expressions and must create a message structure, which is consumable from the [Google Calendar Api](https://developers.google.com/google-apps/calendar/v3/reference/events/insert) 

#### First Idea, using a trigger agent, failed :-1: 

My first idea failed. I want to use the Trigger Agent to extract and reformat data. Unfortunately, the needed date was formatted as long german text and the Google Calendar Publisher Agent needs a date formatted in RFC 3339.  I would have needed some very special liquid filter functions to achieve this way.

### Second try: JavaScript.

But _Huginn_ has a nice JavaScript agent, a swiss knife for all more complex requirements. 

The JavaScript looks like this:

````
function ISODateString(d){
 function pad(n){return n<10 ? '0'+n : n}
 return d.getUTCFullYear()+'-'
      + pad(d.getUTCMonth()+1)+'-'
      + pad(d.getUTCDate())+'T'
      + pad(d.getUTCHours())+':'
      + pad(d.getUTCMinutes())+':'
      + pad(d.getUTCSeconds())+'Z'}

var monthArray = [ "Januar", "Februar", "März", "April", "Mai",
  "Juni", "Juli", "August", "September", "Oktober",
  "November", "Dezember" ]

Agent.receive = function() { 
   var events = this.incomingEvents();
   for(var i = 0; i < events.length; i++) {
    var body = events[i].payload['body']
    var summary = events[i].payload['subject']
    var germanDate = body.match(/\w+, (\d+). (\w+) (\d+)/)
    var day = germanDate[1]
    var month = monthArray.indexOf(germanDate[2])
    var year = germanDate[3]
    var startDate = new Date(year, month, day, 18, 0, 0, 0)
    var endDate = new Date(year, month, day, 21, 0, 0, 0)
    
    this.createEvent(
      { 'message': 
        { 'summary': summary,
          'visibility': 'default',
          'description': body,
          'start': {
           'dateTime': ISODateString(startDate)
          },
          'end': {
            'dateTime': ISODateString(endDate)
          }
        }
      }
    );
  }
}
````

This code fetches the data out of the body of the email and create a data structure consumable from the Google Calendar Publisher Agent. By the way, I love the log statement in JavaScript. This made debugging the script very comfortable. 

### Step 3 - Publish the calendar entry with the Google Calendar Publisher Agent

I have to admit. The Google Calendar Publisher Agent is a tiny shell about the Google Calendar Api. You have to create a message structure with an agent (usually trigger agent) and the Google Publisher send it with your api token to the google interface:

Unfortunately, this Agent doesn't support liquid, so I couldn't separate my credentials from the logic:

I needed a long time, to get the following configuration working. Gently hint: Please authorize the google service email account for modifying your calendar. 

````
{
  "expected_update_period_in_days": "10",
  "calendar_id": "joe@gmail.com",
  "google": {
    "key_file": "/home/huginn/Huginn-en453454343.p12",
    "key_secret": "notasecret",
    "service_account_email": "hugin-443@huginn-43434.iam.gserviceaccount.com"
  }
}
````
### Finally - Every training day I have an event scheduled in my Google Calendar made by _Huginn_

![Event in Google Calendar](https://farm2.staticflickr.com/1482/24635867331_74fd3a8fb9_o.png)

