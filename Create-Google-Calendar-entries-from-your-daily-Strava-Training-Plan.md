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

````