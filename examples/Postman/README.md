# Examples in Postman

## Authentication
In this folder you will find a Postman Collection that exemplifies the Authentication flow when accessing the TransPA Public API.

### Prerequistes
You will need the client id and secret for you application that you've set up inside the [Developer portal](https://oauth.developers.visma.com/). Inside the portal there is a documentation tab where should be able to find all the information you need. A pointer is to read this section about [Service Application](https://oauth.developers.visma.com/service-registry/documentation/authentication#serviceApp) since our API currently only supports Machine-to-Machine integrations.

Also you need to have been granted access to the Sandbox tenant.
Today this is a manual procedure, that will be automated in the future.

### The collection
The Collection consits of two folders: 

#### Basic
There are 3 requests in this folder. The first two are variants for how to retrieve the accesstoken that you will later need to make the alive call.
- Option 1: Get Access Token with credentials assigned as Authorization header (base64 encoded). This option base64 encoding the clientId and clientSecret together with a : in between and allows you to only add 1 environment variable system.
- Option 2: Get Access Token with credentials assigned in the request body. Adds the clientId and clientSecret directly to the request body.
- Reads the Alive call by using the access token that was set previously.

#### Example - Vehicle Resource
- Authenticates and authorizes for the scopes transpaapi:api and transpaapi:vehicles:read
- Reads vehicles

#### The environment file
In order for the example to work you need to provide your client id and client secret, together with the tenant id you want to access. 
In the example the environment file is pre-filled with the Sandbox tenant, so all you need to do is adding the client id and secret.

## Standard Query Example
In this folder you will find a Postman Collection that gives examples on how to use some of our different standard queries in the TransPA Public API.

### Filter
The filter feature allows you to write custom queries. The simplest query is just the choosen field followed by comparator and value. That is:

```
{field}{comparator}{value} => E.g., id$eq:07e9b5d1-83f0-489c-81c5-64427aa959e0
```

If you want to include operator you append them at the end like this:
```
{field}{comparator}{value} => E.g., id$eq:07e9b5d1-83f0-489c-81c5-64427aa959e0$and:status$eq:approved
```

#### Comparators
In the below table you find the comparators we support.

| Comparator | Name                   |
| :-------   | -------:               |
| $eq:       | Equals                 |
| $neq:      | Not equals             |
| $gt:       | Greater than           |
| $gte:      | Greater than or equals |
| $lt:       | Less than              |
| $lte:      | Less than or equals    |

#### Operators
In the table below you find the operators we support.

| Operator | Name     |
| :------- | -------: |
| $and:    | And      |
| $or:     | Or       |