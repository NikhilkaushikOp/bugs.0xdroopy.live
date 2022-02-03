+++
title = "How I Tracked You Around The Globe 🌎"
date = "2021-12-25"
author = "0xdroopy"
theme = "hugo-theme-hello-friend"


+++
## Introduction

Welcome back to my writeups again, I strongly offer my gratitude to you for reading and appreciating my writeups. I was not wondering if I would ever upload a new writeup on this recent report because I only upload less but more meaningful and knowledgeable reports which are distinctively different from many usual people. As you have read my previous writeup, this writeup is also on Google VRP Program. This is because Google is a platform where you can report without any worries of getting it duplicated. This report is on the product of Google named Waze.



## What is Waze?
Waze is a maps platform similar to Google maps. It got acquired by Google many years ago and is still live in the google bug bounty program. It is a truly great map solution which In my opinion is better than Google Maps. The scope of the pen-testing is also very wide to get some vulnerabilities. 

{{< image src="https://www.techstry.net/wp-content/uploads/2021/10/309-waze-pure-dark-mode-is-finally-on-its-way-image.jpeg" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

## How was I able to track anyone?
After usual scanning the application as I usually do every day, I came across a strange endpoint in the HTTP history section of Burp Suite Professional. This endpoint was visible to me as it showed me certain User IDs disclosed. Then I looked at the endpoint, it was like:- 

```
https://www.waze.com/redacted?bbox=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX&language=en-US&v=2&mapComments=true&venueLevel=1&venueFilter=1%2C0%2C0
```

## What's the catch here?
You would be wondering that the listing of users is not that useful thing if found. Yes, it is not that useful that's why I dig deeper. As you can see you would be asking what is this parameter `bbox` has to do here? After certain research, let me explain to you what is bbox?

{{< image src="https://www.ecenglish.com/learnenglish/newsletter/12june/Idiom-whats-the-catch.jpg" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

## What is Bbox?

BBOX is an acronym for Bounding Box. Coordinates of a bounding box are encoded with four values in pixels: [x_min, y_min, x_max, y_max] . x_min and y_min are coordinates of the top-left corner of the bounding box. x_max and y_max are coordinates of the bottom-right corner of the bounding box. This is a cross-section area bounding an area.

{{< image src="https://www.researchgate.net/publication/336760546/figure/fig7/AS:817390560493577@1571892504904/Varying-bounding-box-coordinates.ppm" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

## Exploitation 
Now I was able to sense that something is catchy here. What will happen if I change the bbox in the URL to the bbox of a certain place. Boo-Yah! I was correct here, I was able to see who visited that bbox coordinate or we could say in easier words, who visited that location. I was having a huge list of users along with their user ids which helped me to take a once step more digger into the ground.


## The Evil Attack Scenario
Hmm! the attack scenario is something more interesting than the exploitation of the vulnerable endpoint. Suppose I am an attacker who wants to arrest a person using his location. What can I do is copy his username and find it on the page by entering the bbox coordinates of certain locations. If I wanted to know if a person has visited a certain location suppose `LOCATION A` then I will copy the coordinates and check whether he went there or not. Then if he visited there then I will pick coordinates of all directions near the `LOCATION A` and see where he has gone. Then after a lot of chaining, I would be easily able to track him.

{{< image src="https://cdn.dribbble.com/users/1304577/screenshots/4032985/kiiwik-app-_03.gif" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}


## How Google Looked at this Report?
Google is fast. They access the report as early as possible and give updates on whether it is applicable or not. Within an hour of submitting my report got triaged and after around 1 hour it got Accepted as well. I knew that Google is fast, but this fast? My experience with google was very amazing. Then their message came inside the update mail only, that the finding is very cool and they have passed the bug to the fixing department and I was going to get an update on the bounty after 5 days. Gotcha!

## Conclusion 
Thanks for reading this report, Hope you were able to gain some knowledge after reading it. The advice that I would suggest to my community is to look into the history of requests made after hunting on a program and it would definitely help them. See you in the next write-up very soon! Peace :)

{{< image src="https://media.makeameme.org/created/in-conclusion-it.jpg" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

## Timeline:

[Jan 18, 2022] - Bug reported

[Jan 18, 2022] - Initial triage

[Jan 18, 2022] - Bug accepted (P4 -> P2)

[Jan 23, 2022] - Bug mitigated by temporarily disabling the Moments feature

[Jan 29, 2022] - Reward of $XXXX issued
