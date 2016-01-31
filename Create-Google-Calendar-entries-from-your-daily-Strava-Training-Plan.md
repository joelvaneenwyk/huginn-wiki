### New Year Resolutions: Participate at a marathon and automate my life.

Ok, this sound silly and maybe it is, but I want to use my (poor) coding skills to automate things as far as possible and I want to participate at a marathon this year. Oh and by the way, I am not the youngest person on earth anymore :-)

To prepare for the marathon I started a training plan on [Strava](https://www.strava.com), a platform for fitness enthusiasts. Strava send me a daily instruction for my training via email. But I want the instructions as a google calendar entry, where I organize my life. So I started dealing with Huginn, to gain experience in automating things.

I created in Huginn a workflow like this:

![My workflow](https://farm2.staticflickr.com/1551/24360536849_bf3d68b7e7_o.png)

Scenario:

![Training Plan as scenario](https://farm2.staticflickr.com/1569/24101494863_a87afba574_o.png)

### Step 01: Check my gmail account for a new training plan.

I use the IMAP Folder agent to check several times a day for a new mail from Strava:

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

This agent generates an event with the data of the fetched mail: subject and body. The problem is that the important information is inside the body text of the mail

````

### Step 02 - Extract the information out of the body and create a google calendar message

Now the things become nasty. The information about the training is in the body of the mail. And in the body is the date of next training date. I have to extract the information via regular expressions and needed to create a message structure, which is consumable from the Google Calendar Api. 

#### First Idea, using a trigger agent, failed :-1: 

My first idea failed. I want to use the Trigger Agent to extract and reformat data. Unfortunately, the needed date was formatted in a long german version and the Google Calendar Publisher Agent needs a date formatted in RFC 3339.  Here is room for improvement.

### Second try: JavaScript.

But _Huginn_ has a nice JavaScript agent, a swiss knife for all more complex requirements. The solution looks like this:

````
function ISODateString(d){
 function pad(n){return n<10 ? '0'+n : n}
 return d.getUTCFullYear()+'-'
      + pad(d.getUTCMonth()+1)+'-'
      + pad(d.getUTCDate())+'T'
      + pad(d.getUTCHours())+':'
      + pad(d.getUTCMinutes())+':'
      + pad(d.getUTCSeconds())+'Z'}

var monthArray = [
  "Januar",
  "Februar",
  "März",
  "April",
  "Mai",
  "Juni",
  "Juli",
  "August",
  "September",
  "Oktober",
  "November",
  "Dezember"
  ]

Agent.receive = function() {
  
   var events = this.incomingEvents();
  for(var i = 0; i < events.length; i++) {
    var body = events[i].payload['body']
    var summary = events[i].payload['subject']
    // var findDateExpression = new RegExp("\\w+, (\\d+. \\w+ \\d+)")
    // var germanDate = findDateExpression.exec(body)
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


