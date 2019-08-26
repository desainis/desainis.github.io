---
title: "The Struggle of Creating Something Useful"
published: true
---

# Splink - The Journey

Over the course of the last two to three weeks, I embarked upon a journey to create a Slack bot that helps manage cloud resources. The latest in my ever so "long" list of projects. As a site reliability engineer you know the infrastructure like nothing else. It just felt like having a bot do the day to day operations just made complete sense. Then I thought...why not make a slack app for everyone else? In this post, I'm going to cover the most annoying things I struggled with while building this app. (_Note: this project is still ongoing and has a long way to go_). In short let's go over:

- Architecting an app in 2019
- Keeping security in mind 
- Developing Locally

## Architecting an App 
When you're fresh out of school, you have the mindset of "code!code!code!", building anything useful usually requires a pipeline like:
![software-lifecycle](http://www.mobilecaddy.net/wp-content/uploads/2015/01/Mobile-App-Lifecycle-Flow-2.jpg)

So I began to start to think about the lifecycle of the app before I touched a single piece of code and boy did it get complicated. In the end I landed on:

- NodeJS - Every cloud platform has client libraries in Node. Also Express is cool. 
- MongoDB - The structure of the data is not entirely clear at this stage. A NoSQL database felt like the way to go. 
- Docker (`docker-compose`) - because how else do you deploy applications easily? 

If I had started a project and began writing .. who knows where I would have ended up. So spend some time and think about the underlying applications / infrastructure before you write a piece of code. 

## Keeping Security in Mind
In the day and age of everyday hacks, stolen credit card numbers and personal information. It is always a good idea to always have security in mind (especially with _slack_). Slack in and of itself is not a bad platform, a terribly designed app is bound to be victim to an attack however. In short let's run through some code that verifies the origin of slack requests. First let's walk through a "typical" interaction a user may have with your slack app:
![slack-workflow-app](https://a.slack-edge.com/4389b/img/api/articles/approval_workflows.png)

In this overtly complicated workflow you're assuming every request is coming from "Slack" which need not be true. By merely observing or reading the application code any teenager would be able to deciper that there are no authentication checks in a "standard" application. Let's fix that. Slack provides an [easy way](https://api.slack.com/docs/verifying-requests-from-slack) to authenticate requests. You just need to:

- Fetch the timestamp of the request
- Fetch the raw body of the request
- Ignore any requests that are more than five minutes apart (Replay attacks suck!)
- Compare the requests signature and your SHA256 generated signature. 

```js
// Verify Request Origin
var request_body = req.rawBody;
var timestamp = req.headers['x-slack-request-timestamp'];
if (Math.abs(Math.floor(new Date() / 1000) - timestamp) > 60 * 5) {
    // The request timestamp is more than five minutes from local time.
    // It could be a replay attack, so let's ignore it.
    return false;
};

var sig_basestring = 'v0:' + timestamp + ':' + request_body;
var compute_signature = 'v0=' + crypto.createHmac('sha256', process.env.SLACK_SIGNING_SECRET).update(sig_basestring).digest('hex');
var req_signature = req.headers['x-slack-signature'];
return compute_signature == req_signature;
```

## Developing Locally
Developing a interactive slack app locally was a painful journey. Thankfully, [`ngrok`](https://ngrok.com/) saved me. The tag line explains exactly what it is: `Public URLs for exposing your local web server`. This app runs on port 3000. Install ngrok and run:

```bash
./ngrok http 3000
```

This will provide you with a unique URL for your "local" web server. This can then be configured in your [slack app settings](https://api.slack.com/tutorials/intro-to-message-buttons). From now on, any post requests for interactive messages will be sent to your local web server. Happy Coding!