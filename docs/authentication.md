---
layout: default
title: 🔑 Authentication
nav_order: 2
---

# 🔑 Authentication

The Archipelago API has a combination of unauthenticated and authenticated endpoints available. Each endpoint's documentation specifies whether or not authentication is required.

If authentication is required for a request, you will need to specify the following header that includes your Archipelago API Token: `x-archipelago-frontend-token: [YOUR TOKEN HERE]`.

Example requests that show how to include this header can be found for each necessary endpoint in the [API Routes](api/index.md) section.

If no authentication is required, simply call the API per the documentation.

## To Obtain a Token:

🔒 _Keep this token safe and do not share this token with others, or store it in publicly accessible areas!_

1. Go to the [Archipelago](https://archipelago.art) site and connect your Ethereum wallet
2. Sign the message to grant your token (found in the 'user pages' nav once your wallet is connected)
3. Use your browser dev tools to find the `window.localStorage` data
4. Within the local storage you will find your token: `x-archipelago-frontend-token:{yourAddress}: {yourToken}`
5. Save and use the value -- the `{yourToken}` portion -- as your API token for authenticated requests
