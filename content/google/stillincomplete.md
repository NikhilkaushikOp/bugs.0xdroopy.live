+++
title = "All Accounts Takeover On Tenor Due to No Authorization Of Oauth Token 🍁"
date = "2022-03-12"
author = "0xdroopy"


+++

## Introduction 
{{< image src="https://www.teahub.io/photos/full/106-1060107_famous-paintings-of-the-renaissance-wallpaper-school-of.jpg" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

Hey, People hope you all are doing well! It is been a great time since we met through our daily blogs of my findings on certain programs. For the last three months, I have been stuck to the Google VRP and found something really interesting and critical. The reason I wanted to write about this is because of how much fun I had finding it. This was an unexpected find that caught my attention while testing one of the big acquisitions owned by Google LLC. which is a famous Gif solution named Tenor.
Please note that Tenor has passed its 6 month blackout period which is described by Google allowing it to go for monetary rewards.
## Story


I was looking at one of the acquisitions owned by Google Inc. lately in 2016. After all, recognizing it as a rewardable asset, I began hunting on it. After a bit of observation, I stopped at the Oauth Flow which got my attention even more. After some requests, it came to notice for me that a serious misconfiguration is going on which was helpful for the attacker to take over every single account on tenor.com.

{{< image src="https://momreadit.files.wordpress.com/2021/04/hello-garden-1.jpg" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

This was an unexpected as well as very interesting find and has a severe impact on the users as well as developers using it to make, upload and create awesome gifs. To exploit you should need to deep dive into the requests made during logging into the account on tenor.com using an OAuth functionality. 

## How Oauth Flow Works?

{{< image src="https://developers.google.com/identity/protocols/oauth2/images/flows/authorization-code.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

Oauth is a simple functionality used in many applications to make them sign with the existing account on certain platforms. Google has one of the most famous Oauth which works in almost every application we see in our day-to-day needs. OAuth flow has a very systematic and secure way to make and create the account on specific platforms. There are many OAuth functionalities present, but here we are going to talk about the one which Tenor uses - Authorization Code. 
#### While Clicking Sign In With Google
{{< image src="https://i.ibb.co/Mnc9NKz/hello1.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

{{< image src="https://i.ibb.co/gjf3Lf8/image.png" alt="Hello Friend" position="center" style="border-radius: 10px;" >}}

```HTTP
GET /o/oauth2/auth?redirect_uri=storagerelay%3A%2F%2Fhttps%2Ftenor.com%3Fid%3Dauth251216&response_type=permission%20id_token&scope=email%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Ftenor&openid.realm=&include_granted_scopes=true&client_id=XXXXXXXXXXXXXXXXXXXXXX HTTP/2
Host: accounts.google.com
Cookie: XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:97.0) Gecko/20100101 Firefox/97.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://tenor.com/
Dnt: 1
Upgrade-Insecure-Requests: 1
Sec-Fetch-Dest: document
Sec-Fetch-Mode: navigate
Sec-Fetch-Site: cross-site
Te: trailers
```

#### Selecting Google Account

{{< image src="https://i.ibb.co/0QdVW6s/hello2.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

{{< image src="https://i.ibb.co/gjf3Lf8/image.png" alt="Hello Friend" position="center" style="border-radius: 10px;" >}}

```HTTP
GET /o/oauth2/iframerpc?action=issueToken&response_type=token%20id_token&login_hint=AJDLj6JXrAdwGc8b9pldZZaLHnjbRv3xVIz49lxCkoyi6HA9WkOQWbSqF0MrONvcPKEhKZWphhY294SMOezVRY7_j32MAaN6SQ&client_id=598652403343-harjvt5thjol9qjkrfqpmb7njrnek80v.apps.googleusercontent.com&origin=https%3A%2F%2Ftenor.com&scope=email%20https%3A%2F%2Fwww.googleapis.com%2Fauth%2Ftenor&ss_domain=https%3A%2F%2Ftenor.com&include_granted_scopes=true HTTP/2
Host: accounts.google.com
Cookie: __Host-GAPS=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:97.0) Gecko/20100101 Firefox/97.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
X-Requested-With: XmlHttpRequest
Dnt: 1
Referer: https://accounts.google.com/o/oauth2/iframe
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-origin
Te: trailers
```

#### Response from the server with a request of Oauth Token

```http
POST /keyboard.login HTTP/1.1
Host: api-v1.tenor.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:97.0) Gecko/20100101 Firefox/97.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: https://tenor.com/
Content-Type: application/x-www-form-urlencoded
Origin: https://tenor.com
Content-Length: 997
Dnt: 1
Sec-Fetch-Dest: empty
Sec-Fetch-Mode: cors
Sec-Fetch-Site: same-site
Te: trailers
Connection: close

gaia_token=<Oauth-Token>
```

## What's There In These Requests To Notice?

To further go for exploit I believe you should be aware of what's going on... This gives a clear vision of the vulnerability that you are about to find or are next to. Here in this OAuth Flow, there are simple and beautiful requests made between you, tenor, and accounts.google.com. First Of all, whenever the user clicks the sign in the request is taken to the Tenor. Then Tenor transfers the request from itself to Google to authorize the user with its favorable account. After that Google Authenticates the User and verifies whether the email and password are correct in its Authentication Database or not. As the authentication ends, Google sends the Oauth Token to the tenor and here the role of Google here ends. **After that Tenor authorizes the OAuth token given by Google and extracts the email address from it then checks in its database and then makes the user login.** 

{{< image src="https://i.ibb.co/TK36N5P/image.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

The main thing in this whole flow that we want to notice is the point where the Tenor Authorizes the OAuth token given from Google. The OAuth token received is in the form of `eyj` format by which the Tenor extracts the email address and signs the user in the account.



## The Real Vulnerability

{{< image src="https://media.istockphoto.com/illustrations/night-sea-after-storm-with-sailboat-painting-illustration-id473421132?k=20&m=473421132&s=612x612&w=0&h=ZGEUa6fA6cTja7LwuE4jEHacOjEZdel6jDl4QRgX2DA=" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

In this lovely and enjoyable process of OAuth, there is something that goes very wrong at tenor.com. The Backend API fails to authorize the OAuth token which was provided by the **Google** by which we could authorize the tokens from the third-party platforms. What does that third party mean? Does it refer that what if we take the token from another website and use it here? This makes everything very critical as almost every company uses the OAuth functionality to make its users get signed in to its platform. And also these companies store the Access Tokens as well. Now Suppose if an account is created on tenor.com and then it is created on a third party app then the third party app would be able to take over the account successfully. By this, it turns out to be a major threat as anyone can make a website where they allow OAuth authentication and then they could use the token which they received from the user.




## The Conclusion!

{{< image src="https://media.makeameme.org/created/one-does-not-5b6956.jpg" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}




## Timeline:

[Dec 24, 2021] - Bug reported

[Dec 24, 2021] - Initial triage

[Dec 24, 2021] - Bug accepted (P4 -> P2)

[Jan 02, 2022] - 

[Jan 14, 2022] - 
