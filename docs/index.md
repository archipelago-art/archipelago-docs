# Archipelago API Overview
The Archipelago API is a REST-based API to facilitate transactions and retrieve information on the Archipelago marketplace.

## Base Path 
The API base path is: `https://api.archipelago.art/:version`

Currently `v1` is the latest and only version, so all API calls should be made to `https://api.archipelago.art/v1`

All requests must be made over HTTPS.

## Authentication
The Archipelago API has a combination of unauthenticated and authenticated endpoints available. Each endpoint's documentation specifies whether or not authentication is required.

If authentication is required for a request, you will need to specify the following header that includes your Archipelago API Token: `x-archipelago-frontend-token: [YOUR TOKEN HERE]`. 

Example requests that show how to include this header can be found for each necessary endpoint in the [Resources & Routes](#-Resources-amp-Routes) documentation below.

If no authentication is required, simply call the API per the documentation.


### To Obtain a Token:

:lock: *Keep this token safe and do not share this token with others, or store it in publicly accessible areas!*

1. Go to [Archipelago](https://archipelago.art) and connect your Ethereum wallet
3. Sign the message to grant your token (found in the 'user pages' nav once your wallet is connected)
4. Use your browser dev tools to find the `window.localStorage` data
5. Within the local storage you will find your token: `x-archipelago-frontend-token:{yourAddress}: {yourToken}`
6. Save and use the value -- the `{yourToken}` portion -- as your API token for authenticated requests


## Errors
Archipelago uses the conventional HTTP response codes to indicate the success or failure of an API request.