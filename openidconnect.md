# OpenId connect

- Oauth2 (delegation protocol)
- JOSE (json object signin and encryption)
- OpenID

## Oauth2 diagram

- IDP = identity provider (has protected resource, ex. gitlab, github, LDAP)
- RP = relying party (oauth2 client)
- PR = protected resource (the resource that is protected)

IDP -> RP

- IDP sends access token to RP and that is the same as in oauth2
- ID token (JWT)
- OpenID scope for client that generates ID token
- OpenID audience
  - for access token is protected resource
  
  PR needs to know what acess token is good for, there are in genreal 2
  mechanisms to do that:
  
  - it's written in token itself(JWT)
  - IDP supports token introspection

### ID Token

- Who token is issued to
- Who authorized it
- Who has issued it
- When it expires

### How to convert to openid connect

- When request token add scope for openid connect
- Take ID token and use JOSE specs to parse it and check claims in ID token
- 2 claims (issuer, subject)
  - issuer: url identifier of identity provider (LDAP, github, gitlab)
  - subject: unique for the user talking about
  
User profile endpoint in IDp, returns openid standard response about user
we perform auth for.

### When do you need openid connect

- when you need identity besides authentication
- You need stanard way to get user information (email, address, location, phone number, ...)
