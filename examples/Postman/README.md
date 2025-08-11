# Examples in Postman

## Authentication
This folder contains a Postman Collection that exemplifies the authentication flow for accessing the TransPA Public API.

### Prerequistes
You will need the client id and secret for you application that you've set up inside the [Developer portal](https://oauth.developers.visma.com/). Inside the portal there is a documentation tab where should be able to find all the information you need. A pointer is to read this section about [Service Application](https://oauth.developers.visma.com/service-registry/documentation/authentication#serviceApp) since our API currently only supports Machine-to-Machine integrations.

Also you need to have been granted access to the Sandbox tenant.
Today this is a manual procedure, that will be automated in the future.

#### The environment file
For the examples to work, you must provide your client ID, client secret, and the tenant ID in the Postman environment file. The environment is pre-filled with the Sandbox tenant ID, so you only need to add your client credentials.

### The collection
The Collection consists of two folders: 

#### Basic
There are 3 requests in this folder. The first two are variants for how to retrieve the accesstoken that you will later need to make the alive call.
- Option 1: Get Access Token (Authorization header): Retrieves the token using a Base64 encoded string of your clientId:clientSecret in the Authorization header. Allows you to only add 1 environment variable in your system.
- Option 2: Get Access Token (Request Body): Retrieves the token by sending the clientId and clientSecret directly in the request body.
- Alive Check: A simple API call to verify that the access token is working correctly.

#### Example - Vehicle Resource
- Authenticates and authorizes using the scopes transpaapi:api and transpaapi:vehicles:read
- Reads vehicles data

## Standard Query Example
This folder contains a Postman Collection that gives examples on how to use some of our different standard queries in the TransPA Public API.

### Cursor Pagination
This folder demonstrates how cursor-basen pagination works. Cursors are used to retrieve subsequent pages of a resource collection. 

When you request a collection and the number of items exceeds the page limit. the response body will contain a nextToken. To fetch the next page, add this value as a cursor query parameter in your next request.

Important: Any other query parameters from the original request (like filter or limit) must be included in subsequent requests as well.
```
?cursor={nextToken}
```

### Filter
The filter feature allows you to write custom queries. The basic syntax is {field}{comparator}{value}.
```
?filter={field}{comparator}{value}
// Example: ?filter=id$eq:07e9b5d1-83f0-489c-81c5-64427aa959e0
```

To combine multiple filter conditions, append a logical operator and the next condition.

```
?filter={field}{comparator}{value}{operator}{field}{comparator}{value}
// Example: ?filter=id$eq:07e9b5d1-83f0-489c-81c5-64427aa959e0$and:status$eq:approved
```

#### Comparators
The following comparators are supported.

| Comparator | Name                   |
| :-------   | -------:               |
| $eq:       | Equals                 |
| $neq:      | Not equals             |
| $gt:       | Greater than           |
| $gte:      | Greater than or equals |
| $lt:       | Less than              |
| $lte:      | Less than or equals    |

#### Operators
The following logical operators are supported for combining conditions.

| Operator | Name     |
| :------- | -------: |
| $and:    | And      |
| $or:     | Or       |