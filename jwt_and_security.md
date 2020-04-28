# JWT/Passport and Security

## JSON Web Tokens (JWT)
Many web applications and APIs use a form of authentication to protect resources and restrict their access only to verified users. This guide will walk you through how to implement authentication for an API using Json Web Tokens (JWTs) and Passport, an authentication middleware for Node.
Understanding JSON Web Tokens

JSON Web Token (JWT) is an open standard that defines a compact and self-contained way for securely transmitting information between parties as a JSON object.

JWTs are secure because they are digitally signed and if the information
contained within is tampered in any way, it renders that token invalid. JWTs also support an expiration time so as a developer you can specify how frequently you want them to have to re-authenticate (seconds, hours, days, etc.). When a token that was originally valid expires, it is equally considered invalid and the user must re-authenticate.

A JWT is composed of three separate definitions: `header`, `payload`, and `signature`. In class we will deal mainly with the `payload` section. The `payload` section is where we can tuck any information we want in the JWT that we will extract later when deciding if the authenticating user should have access to some endpoint or other resource 

`Header` : The header defines the type of algorithm used to verify the token and the type of token. In this example we are using 256 bit algorithm.
```
{
   "type" : "JWT",
   "alg" : "HS256"
 }
```
`Payload`: The `payload` contains the claims. Claims are information about the user together with other additional metadata that we will extract later to determine if the request and the requesting user should be able to access whatever resource. *We will use this the most in class*
```
{
   userName: 'Kevin',
   userEmail : 'kyancy@anywhere.com',
   userId: 2112
 }
```

`Signature` : The signature encodes the information in the header and payload in base64 format together with a secret key. All this information is then signed by the algorithm specified in the header. In our example, we’re using HMACSHA256. The signature verifies that the message being sent wasn’t tampered along the way.
```
HMACSHA256(
   base64UrlEncode(header) + "." +
   base64UrlEncode(payload),
   superSecretKeyPhraseString
 )
```

> *NOTE:* JWT, like any technology isn't hack proof. If someone intercepts the token being sent from the client to the server, they still can conceivably decrypt it so DO NOT send super secure info like social security numbers or similar!

## Passport
Passport is an authentication middleware used to authenticate requests. It allows developers to use different *strategies* for authenticating users, such as using a local database or connecting to single sign-on servers (SSO) through APIs.

## Installing Dependencies we Need
Before we can implement this on our server-side, we need to install some additional dependenices in addition to the common dependencies we use like `express`. The following command will get you all we need for the class. *Be sure* that you are in your `server` directory prior to installing these modules.

```
npm install bcrypt body-parser express jsonwebtoken mongoose passport passport-local passport-jwt
```

