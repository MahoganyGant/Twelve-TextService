# Twelve-TextService

Twelve AI Assistant — Setup Guide
Get your text buddy running in about 30 minutes.

What You Need

A Replit account (you have this)
An Anthropic API key — platform.anthropic.com
A Twilio account — twilio.com (free trial gives you a number immediately)


Step 1 — Create the Replit Project

Go to replit.com and create a new Repl
Choose Node.js as the template
Name it something like twelve-assistant
Upload these files: index.js, package.json


Step 2 — Add Your Secrets
In Replit, click the lock icon in the left sidebar (Secrets). Add these four:
Secret NameWhere to find itANTHROPIC_API_KEYplatform.anthropic.com → API KeysTWILIO_ACCOUNT_SIDtwilio.com → Console DashboardTWILIO_AUTH_TOKENtwilio.com → Console DashboardTWILIO_PHONE_NUMBERYour Twilio number in +1XXXXXXXXXX format

Step 3 — Get a Twilio Number

Go to twilio.com and create a free account
Verify your personal phone number (required for trial)
Go to Console → Phone Numbers → Manage → Buy a Number
Search for a number, grab one — free trial gives you $15 credit
Copy the number in +1XXXXXXXXXX format → paste as your TWILIO_PHONE_NUMBER secret


Step 4 — Run the Project
In Replit, click Run. You should see:
Twelve assistant running on port 3000
Replit will give you a public URL that looks like:
https://twelve-assistant.yourusername.repl.co
Copy that URL — you need it for the next step.

Step 5 — Connect Twilio to Your Server
This is the step that makes texts actually reach your server.

In Twilio Console → Phone Numbers → Manage → Active Numbers
Click your number
Scroll to Messaging Configuration
Under "A message comes in" → set to Webhook
Paste your Replit URL + /sms:

   https://twelve-assistant.yourusername.repl.co/sms

Method: HTTP POST
Save


Step 6 — Test It
Text your Twilio number from your personal phone.
On Twilio free trial, you can only text numbers you've verified. Your personal number is already verified from signup.
You should get a response back in the assistant's voice within a few seconds.

Important: Keep Your Repl Awake
Replit free tier puts projects to sleep after inactivity. When it sleeps, texts won't get responses.
Option A (free): Use UptimeRobot (uptimerobot.com) — create a free monitor that pings your Replit URL every 5 minutes. This keeps it awake.
Option B (paid): Upgrade to Replit's Hacker plan which keeps Repls always-on.
Option C: Deploy to Railway (railway.app) instead — $5/month, always-on, easier for this use case.

Sending Proactive Messages (Optional)
To have the assistant text YOU first, hit the /send-proactive endpoint:
bashcurl -X POST https://your-repl-url.repl.co/send-proactive \
  -H "Content-Type: application/json" \
  -d '{"to": "+1yournumber", "trigger": "no_login_3days"}'
Available triggers:

no_login_3days — light check-in after 3 days
no_login_7days — soft re-engagement after a week
cycle_complete — acknowledges finishing a cycle
cycle_midpoint — fragile middle check-in around week 6

You can automate these with a free cron service like cron-job.org or Replit's built-in scheduled tasks.

Costs (Realistic Estimate)
ServiceCostClaude API (Haiku)~$1-3/month for daily useTwilio SMS~$1.15/month for number + ~$0.01/messageReplit (keep-awake)Free with UptimeRobot trickTotal~$5-10/month

What's Next (When You're Ready)
Once this is running and you've tested the personality:

Add Replit DB for persistent conversation storage (right now memory resets if the server restarts)
Build API endpoints on your Twelve app that expose your cycle data
Connect the data so the assistant can reference your actual habit completion, friction patterns, identity work
Add more proactive triggers tied to real app events

But get the text buddy running first. Test it on yourself through your cycle transition. That's the point right now.
