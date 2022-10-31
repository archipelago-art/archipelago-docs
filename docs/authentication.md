---
layout: default
title: Authentication
nav_order: 2
---

# 🔑 Authentication

The majority of the Archipelago APIs do not require any authentication for normal use. However, there are some endpoints that require authentication. This page will explain how to authenticate with the Archipelago APIs.

If authentication is required for a request, you will need to specify the following header that includes your Archipelago API Token: `x-archipelago-frontend-token: [YOUR TOKEN HERE]`.

Any route where authentication is necessary will indicate so. Sample code of how to perform the request is also included. For one example, see the [GET `/user/info`](api/user_routes.md#get-userinfo) route.

If no authentication is required, simply call the API per the documentation and sample code.

## To Obtain a Token:

{: .warning-title }
> 🔒 Keep This Private
> 
> This token is private and should not be shared with anyone. It should also not be stored in publicly accessible areas.

1. Go to the [Archipelago](https://archipelago.art) site and connect your Ethereum wallet
   1. Each Ethereum wallet will have a unique token
2. Sign the message to grant your token (found in the 'user pages' nav once your wallet is connected)
3. Use your browser dev tools to find the `window.localStorage` data
4. Within the local storage you will find your token: `x-archipelago-frontend-token:{yourAddress}: {yourToken}`
   1. Note: Your token is a UUID (e.g. `a0b1c2d3-e4f5-6g7h-8i9j-0k1l2m3n4o5p`)
   2. Note: You may see multiple tokens, one for each Ethereum address you have connected to Archipelago
5. Save and use the value -- the `{yourToken}` UUID portion -- as your API token for authenticated requests
