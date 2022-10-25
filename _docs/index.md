# Archipelago API Overview
The Archipelago API is a REST-based API to facilitate transactions and retrieve information on the Archipelago marketplace.

## :information_source: Base Path 
The API base path is: `https://api.archipelago.art/:version`

Currently `v1` is the latest and only version, so all API calls should be made to `https://api.archipelago.art/v1`

All requests must be made over HTTPS.

## :key: Authentication
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


## :warning: Errors
Archipelago uses the conventional HTTP response codes to indicate the success or failure of an API request.

### Status Codes
| Status Code            | Summary                                      |
| ---------------------- | -------------------------------------------- |
| **200** - OK           | Everything worked as expected.               |
| **400** - Bad Request  | The request was not structured properly.     |
| **401** - Unauthorized | No valid API key was provided.               |
| **404** - Not Found    | The requested API resource was not found.    |
| **500** - Server Error | Something went wrong on the Archipelago end. |

## :racehorse: Rate Limits
The Archipelago API does enforce rate limits for each client. Every response from the Archipelago API includes two headers related to rate limits:
- `x-rate-limit-max`: the maximum request limit for your token, by default this is `40`
- `x-rate-limit-remaining`: the capacity remaining out of the total limit

The `x-rate-limit-remaining` header will change based on the number of requests made. 

**Importantly**, if the rate limit is reached, a 429 HTTP error code will be returned from the API. 

# Object Types
These are the different objects that will be found in the Archipelago API. Documentation in an individual route will likely reference one or more of these objects.

## Collection Objects

### `CollectionInfo` Object
| Name                    | Type     | Description                                                                 |
| ----------------------- | -------- | --------------------------------------------------------------------------- |
| `projectId`             | `string` | The unique id of the collection.                                            |
| `slug`                  | `string` | The unique text slug of the collection.                                     |
| `artblocksProjectIndex` | `string` | The project index on artblocks.                                             |
| `imageUrlTemplate`      | `string` | The template to use to retrieve an image for a token within the collection. |
| `name`                  | `string` | The name of the collection.                                                 |
| `artistName`            | `string` | The artist's name.                                                          |
| `description`           | `string` | The description of the collection.                                          |
| `aspectRatio`           | `string` | The aspect ratio of token images in the collection.                         |
| `numTokens`             | `string` | The number of tokens that have been minted in the collection.               |
| `maxInvocations`        | `string` | The total possible number of tokens that can exist in the collection.       |
| `tokenContract`         | `string` | The address of the contract.                                                |
| `fees`                  | `array`  | A list of `CollectionFees` objects for the collection.                      |
| `tokens`                | `array`  | A list of `CollectionToken` objects in the collection.                      |

### `CollectionFees` Object
| Name     | Type     | Description                            |
| -------- | -------- | -------------------------------------- |
| `target` | `string` | The target address to send the fee to. |
| `micros` | `string` | The amount of the fee.                 |
| `static` | `string` | A boolean `true|false`.                |

### `CollectionToken` Object
| Name         | Type     | Description                                      |
| ------------ | -------- | ------------------------------------------------ |
| `tokenId`    | `string` | The unique id of a token.                        |
| `tokenIndex` | `string` | The unique index of a token within a collection. |

### `CollectionFeature` Object
| Name        | Type     | Description                          |
| ----------- | -------- | ------------------------------------ |
| `featureId` | `string` | The unique id of the feature.        |
| `name`      | `string` | The name of the feature.             |
| `traits`    | `array`  | A list of `CollectionTrait` objects. |

### `CollectionTrait` Object
| Name           | Type     | Description                                     |
| -------------- | -------- | ----------------------------------------------- |
| `traitId`      | `string` | The unique id of the trait.                     |
| `value`        | `string` | The value of the trait.                         |
| `tokenIndices` | `array`  | A list of tokenIndices that contain this trait. |
| `slug`         | `string` | The unique slug of the trait.                   |

### `CollectionAsk` Object
| Name          | Type     | Description                                            |
| ------------- | -------- | ------------------------------------------------------ |
| `priceWei`    | `string` | The asking price (in WEI) for the token.               |
| `listingTime` | `string` | The time the ask was listed.                           |
| `venue`       | `array`  | The venue or marketplace that the ask originated from. |

### `CollectionSale` Object
| Name       | Type     | Description                               |
| ---------- | -------- | ----------------------------------------- |
| `tokenId`  | `string` | The ID of the token that was sold.        |
| `saleTime` | `string` | The timestamp that the sale was made.     |
| `priceWei` | `array`  | The purchase amount (in WEI) of the sale. |


## Token Objects

### `TokenInfo` Object
| Name             | Type     | Description                                                                   |
| ---------------- | -------- | ----------------------------------------------------------------------------- |
| `tokenId`        | `string` | The unique id of the token.                                                   |
| `collectionInfo` | `object` | A `CollectionInfo` object with information about the parent collection.       |
| `features`       | `array`  | The project index on artblocks.                                               |
| `history`        | `array`  | The template to use to retrieve an image for a token within the collection.   |
| `currentOwner`   | `string` | The name of the collection.                                                   |
| `chainData`      | `object` | A simple object containing the `tokenContract` address and `onChainTokenId`.  |
| `asks`           | `object` | A wrapper object that potentially contains a list of `CollectionAsk` objects. |
| `bids`           | `object` | A wrapper object that potentially contains a list of `CollectionBid` objects  |

### `TokenTrait` Object
| Name          | Type     | Description                             |
| ------------- | -------- | --------------------------------------- |
| `featureId`   | `string` | The unique id of the collection.        |
| `name`        | `string` | The unique text slug of the collection. |
| `traitId`     | `array`  | The project index on artblocks.         |
| `value`       | `string` | The project index on artblocks.         |
| `featureSlug` | `string` | The project index on artblocks.         |
| `traitSlug`   | `string` | The project index on artblocks.         |

### `TokenHistory` Object
| Name              | Type      | Description                                                                |
| ----------------- | --------- | -------------------------------------------------------------------------- |
| `type`            | `string`  | The type of history event, enum values include `TRANSFER`, `OPENSEA_SALE`  |
| `blockNumber`     | `string`  | The block number.                                                          |
| `logIndex`        | `integer` | The log index.                                                             |
| `transactionHash` | `string`  | The transaction hash representing the history event taking place on-chain. |
| `timestamp`       | `string`  | Time time of the history event (in ISO-8601 format).                       |
| `from`            | `string`  | The address initiating the event.                                          |
| `to`              | `string`  | The address that is the recipient of the event.                            |

## User Objects

### `User` Object
| Name          | Type     | Description                                  |
| ------------- | -------- | -------------------------------------------- |
| `account`     | `string` | The Ethereum address associated to the user. |
| `email`       | `string` | The user's email address.                    |
| `preferences` | `string` | The user's preferences.                      |

### `UserBid` Object
| Name        | Type     | Description                                                          |
| ----------- | -------- | -------------------------------------------------------------------- |
| `bidId`     | `string` | The unique id of the bid.                                            |
| `slug`      | `string` | The slug of the collection that the bid is for.                      |
| `name`      | `string` | The name of the collection that the bid is for.                      |
| `price`     | `string` | The price of the bid.                                                |
| `deadline`  | `string` | The ISO-8601 formatted `datetime` string of when the bid expires.    |
| `bidder`    | `string` | The address of the bidder.                                           |
| `nonce`     | `string` | The nonce associated with the bid.                                   |
| `signature` | `string` | The on-chain signature data for the bid.                             |
| `message`   | `string` | The on-chain message data for the bid.                               |
| `agreement` | `string` | The on-chain agreement data for the bid.                             |
| `scope`     | `string` | The scope for the bid, can be one of `PROJECT`, `TRAIT`, or `TOKEN`. |

### `BidScope` Object
| Name         | Type     | Description                                  |
| ------------ | -------- | -------------------------------------------- |
| `type`       | `string` | The Ethereum address associated to the user. |
| `tokenIndex` | `string` | The user's email address.                    |
| `tokenId`    | `string` | The user's preferences.                      |
| `slug`       | `string` | The user's preferences.                      |
| `name`       | `string` | The user's preferences.                      |


# :arrow_up: API Routes
There are two main resources that are the base of the Archipelago API: **Market** and **User**

The overall hierarchy of the Archipelago API is structured as follows:
```
https://api.archipelago.art/v1
|  market
|  |- collections
|  |- orders
|  user
``` 


## :chart_with_upwards_trend: Market Routes
The base-level market routes contain endpoints to retrieve information about the overall market (views, volume, floors, and more).

### GET `/market/views`

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/views
```

#### Example Response
```json
{
  "185183": {
    "page": "/collections/185183",
    "visitors": 1,
    "collection": "185183"
  },
  "fidenza": {
    "page": "/collections/fidenza",
    "visitors": 279,
    "collection": "fidenza"
  },
  "100-print": {
    "page": "/collections/100-print",
    "visitors": 269,
    "collection": "100-print"
  },
  "ringers": {
    "page": "/collections/ringers",
    "visitors": 100,
    "collection": "ringers"
  },
  "chromie-squiggle": {
    "page": "/collections/chromie-squiggle",
    "visitors": 97,
    "collection": "chromie-squiggle"
  },
  ...
}
```

### GET `/market/volume`
Returns the market volume (total sales, in WEI) for each collection on the Archipelago marketplace. The required `duration` query parameter determines the period of time that the volume is calculated for.

#### Request Parameters
| Name       | Type     | Parameter Type | Required? | Description                                                                   |
| ---------- | -------- | -------------- | --------- | ----------------------------------------------------------------------------- |
| `duration` | `string` | `query`        | Yes       | The duration to lookback. Must be one of the three values: `24h`, `7d`, `30d` |


#### Example Request
```bash
curl --request GET \
  --url 'https://api.archipelago.art/v1/market/volume?duration=24h'
```

#### Example Response
This key of the response object is the collection `slug` and the value is the market volume in WEI.

```json
{
  "8": "0",
  "4444": "0",
  "chromie-squiggle": "12369999999999999000",
  "singularity": "2510000000000000000",
  ...
}
```


### GET `/market/floor-asks`
Returns the floor ask for each collection.

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/floor-asks
```

#### Example Response
This key of the response object is the collection `slug` and the value is an object with the basic ask details.
Additional information is included if the ask is on Archipelago vs. another marketplace.

```json
{
  "8": {
    "projectId": "683915793512766073",
    "tokenIndex": 32,
    "price": "390000000000000000",
    "venue": "OPENSEA"
  },
  "parnassus": {
    "projectId": "685105353981211845",
    "tokenIndex": 62,
    "askId": "2126333717251827583",
    "asker": "0x764aBE778aa96Cd04972444a8E1DB83dF13f7E66",
    "price": "7900000000000000000",
    "venue": "ARCHIPELAGO"
  },
  ...
}
```

### GET `/market/floor-bids`
Returns the floor bid (price, in WEI) for each collection. Any floor bid is a `PROJECT` level bid.

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/floor-bids
```

#### Example Response
This key of the response object is the collection `slug` and the value is an object with the basic bid details.

```json
{
  "chromie-squiggle": {
    "price": "2000000000000000000",
    "projectId": "683915793512607080",
    "bidId": "1838088763269094700",
    "bidder": "0x84aeccde4c9f217e83d3fa28c31d34378b903f91"
  },
  "unigrids": {
    "price": "500000000000000000",
    "projectId": "683915793512674207",
    "bidId": "1838025901333080752",
    "bidder": "0x74fa1be357bc182c88ba77e771a5502e2b271f1b"
  },
  ...
}
```

### GET `/market/bids/:bidId`
Returns the details of a specific bid.

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/bids/1837909952121726225
```

#### Example Response

```json
{
  "bidId": "1837909952121726225",
  "slug": "edifice",
  "name": "Edifice",
  "price": "1850000000000000000",
  "deadline": "2022-07-07T16:20:02.000Z",
  "bidder": "0xFF5aE008713bA824376e7d36F5125429527e12cE",
  "nonce": "1655769242275",
  "signatureData": {
    "message": "0x00000000000000000000000000000000000000000000000000000000000000201339015b7c39bdfb9c269794097dc3313a0f40ace138f6a963cb3f2fb313cd830000000000000000000000000000000000000000000000000000018183899aa30000000000000000000000000000000000000000000000000000000062c707b200000000000000000000000000000000000000000000000000000000000000c000000000000000000000000000000000000000000000000000000000000000e0000000000000000000000000a6ae1c1dc3024ec951972a10a7043bc7425f1f5700000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000020bbda0f451ebadd383ccdc78883e3d09548f05ef5073b9f0c74138a602c03dc00",
    "signature": "0xb20598284ab4814124ddd5c3f3fbb5375ef88323d0cfd0dba2493f8a10e6ffaa187e54fa094b9b86d9b9f15eafa488eef8cec43850aea76c6400c4cbed54c6581c",
    "agreement": "0x0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc200000000000000000000000000000000000000000000000019ac8532c2790000000000000000000000000000a7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd27000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000002a76456bb6abc50fb38e17c042026bc27a95c33140000000000000000800013888a3f65ef24021d401815792c4b65676fbf90663c00000000000061a8000124f8"
  },
  "scope": {
    "type": "PROJECT",
    "scope": "683915793512807811"
  }
}
```

### GET `/market/asks/:ask`
Returns the details of a specific ask

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/asks/2126219693463423900
```

#### Example Response

```json
{
  "askId": "2126334634867702361",
  "slug": "bent",
  "name": "Bent",
  "price": "5000000000000000000",
  "createTime": "2022-07-27T23:54:51.898Z",
  "deadline": "2022-08-10T23:54:44.000Z",
  "asker": "0xE155eB13d4a5Ee61FA7D7015451bCAFE3b364A53",
  "nonce": "1658966084476",
  "tokenId": "395685422044928721",
  "tokenIndex": 235,
  "signatureData": {
    "message": "0x0000000000000000000000000000000000000000000000000000000000000020b87576125507f3ab508b8972af3f7941ea3311c7708dc0fa5cdca72b885eb1470000000000000000000000000000000000000000000000000000018242158b7c0000000000000000000000000000000000000000000000000000000062f4454400000000000000000000000000000000000000000000000000000000000000e0000000000000000000000000000000000000000000000000000000000cc1626b000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
    "signature": "0x7f1363e6e4f3b148e5a85a17dc0827d5740d3ca780feac95412eea1b0c47ae7212326a7ffec1109a16dce6410961667e9e028bf3aea59661cb33ca7b65d813361c",
    "agreement": "0x0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc20000000000000000000000000000000000000000000000004563918244f40000000000000000000000000000a7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd27000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000002a76456bb6abc50fb38e17c042026bc27a95c33140000000000000000800013888a3f65ef24021d401815792c4b65676fbf90663c00000000000061a8000124f8"
  }
}
```


## :page_facing_up: Orders Routes
The orders routes contain endpoints to place orders on the Archipelago marketplace.

### POST `/market/orders`
:construction: Coming soon!


## :art: Collections Routes 
The collections routes contain endpoints to retrieve information about collections and the tokens within them.

### GET `/market/collections`
Returns a list of top-level information (as `CollectionInfo` objects) for all Archipelago supported collections.

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections
```

#### Example Response
```json
[
  {
    "projectId": "683915793512607080",
    "slug": "chromie-squiggle",
    "artblocksProjectIndex": 0,
    "imageUrlTemplate": "https://img.archipelago.art/artblocks/{sz}/0/{hi}/{lo}",
    "name": "Chromie Squiggle",
    "artistName": "Snowfro",
    "description": "Simple and easily identifiable, each squiggle embodies the soul of the Art Blocks platform. Consider each my personal signature as an artist, developer, and tinkerer. Public minting of the Chromie Squiggle is permanently paused. They are now reserved for manual distribution to collectors and community members over a longer period of time. Please visit OpenSea to explore Squiggles available on the secondary market. ",
    "aspectRatio": 1.5,
    "numTokens": 9625,
    "maxInvocations": 10000,
    "tokenContract": "0x059EDD72Cd353dF5106D2B9cC5ab83a52287aC3a",
    "fees": [
      {
        "target": "0x1212121212121212121212121212121212121212",
        "micros": 5000,
        "static": true
      },
      {
        "target": "0x3434343434343434343434343434343434343434",
        "micros": 5000,
        "static": true
      },
      {
        "target": "0x5656565656565656565656565656565656565656",
        "micros": 75000,
        "static": false
      }
    ]
  },
  ...
]
```

### GET `/market/collections/:slug`
Returns the top-level details (as a `CollectionInfo` object) of a single collection, as well as a list of the tokens (as `CollectionToken` objects) in the collection.

#### Request Parameters
| Name   | Type     | Parameter Type | Required? | Description                                                                                      |
| ------ | -------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug` | `string` | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/ringers
```

#### Example Response
```json
{
  "info": {
    "projectId": "683915793512716837",
    "slug": "ringers",
    "artblocksProjectIndex": 13,
    "imageUrlTemplate": "https://img.archipelago.art/artblocks/{sz}/13/{hi}/{lo}",
    "name": "Ringers",
    "artistName": "Dmitri Cherniak",
    "description": "There are an almost infinite number of ways to wrap a string around a set of pegs. On the surface it may seem like a simple concept but prepare to be surprised and delighted at the variety of combinations the algorithm can produce. Each output from 'Ringers' is derived from a unique transaction hash and generated in Javascript in the browser. Feature variations include peg count, sizing, layout, wrap orientation, and a few colorful flourishes for good measure.",
    "aspectRatio": 1,
    "numTokens": 1000,
    "maxInvocations": 1000,
    "tokenContract": "0xa7d8d9ef8D8Ce8992Df33D8b8CF4Aebabd5bD270",
    "fees": [
      {
        "target": "0x1212121212121212121212121212121212121212",
        "micros": 5000,
        "static": true
      },
      {
        "target": "0x3434343434343434343434343434343434343434",
        "micros": 5000,
        "static": true
      },
      {
        "target": "0x5656565656565656565656565656565656565656",
        "micros": 75000,
        "static": false
      }
    ]
  },
  "tokens": [
    {
      "tokenId": "395685417420101184",
      "tokenIndex": 0
    },
    {
      "tokenId": "395685417420105214",
      "tokenIndex": 1
    },
    ...
  ]
}
    
```

### GET `/market/collections/:slug/features`
Returns the features and traits of a single collection (as a `CollectionFeature` object, as well as a list of each token that has a given trait.

#### Request Parameters
| Name   | Type     | Parameter Type | Required? | Description                                                                                      |
| ------ | -------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug` | `string` | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/ringers/features
```

#### Example Response
```json
[
  {
    "featureId": "972146174609730698",
    "name": "Background",
    "traits": [
      {
        "traitId": "1260376550778397709",
        "value": "Beige",
        "tokenIndices": [
          27,
          38,
          79,
          ...
        ],
        "slug": "beige"
      },
      {
        "traitId": "1260376550778386488",
        "value": "Black",
        "tokenIndices": [
          50,
          80,
          220,
          ...
        ],
        "slug": "black"
      },
      ...
    },
    {
      "featureId": "972146174609723031",
      "name": "Body",
      "traits": [
        {
          "traitId": "1260376550778391869",
          "value": "Black",
          "tokenIndices": [
            1,
            2,
            3,
            ...
          ]
        }
      ]
    },
    ...
  }
]
```

### GET `/market/collections/:slug/asks`
Returns the lowest ask (price) for each token in a collection that has at least one active ask. They key of the 'asks' object is the `tokenIndex` that the ask is associated to.

#### Request Parameters
| Name   | Type     | Parameter Type | Required? | Description                                                                                      |
| ------ | -------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug` | `string` | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/fidenza/asks
```

#### Example Response
```json
{
  "asks": {
    "6": {
      "asker": "0x5f9D41289AD44D17e6C51f889276999112e4ffFC",
      "askId": "opensea:7181178876",
      "price": "11500000000000000000",
      "createTime": "2022-07-22T02:12:55.000Z",
      "deadline": "2022-08-22T02:12:55.000Z",
      "tokenId": "396446910998149770",
      "venue": "OPENSEA"
    },
    "57": {
      "askId": "2126271733389438134",
      "price": "14000000000000000000",
      "createTime": "2022-07-16T21:18:11.460Z",
      "deadline": "2022-08-15T21:17:55.000Z",
      "asker": "0xba7647aEC05Ff875ef63b1e99B8477144e82Af0B",
      "tokenId": "396446926994020535",
      "venue": "ARCHIPELAGO"
    },
    ...
  }
}
```

### GET `/market/collections/:slug/bids`
Returns the highest bid for each token in a collection that has at least one active bid. They key of the 'bids' object is the `tokenIndex` that the bid is associated to.

#### Request Parameters
| Name   | Type     | Parameter Type | Required? | Description                                                                                      |
| ------ | -------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug` | `string` | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/chromie-squiggle/bids
```

#### Example Response
```json
{
  "bids": {
    "0": {
      "tokenIndex": 0,
      "tokenId": "395685417968158795",
      "price": "80000000000000000000",
      "deadline": "2022-08-10T15:16:22.000Z",
      "bidder": "0x585f4fBe2d2A889c286fa71FB81D01f30773F4B1",
      "bidId": "1838102220161507163"
    },
    "1": {
      "tokenIndex": 1,
      "tokenId": "395685417968189553",
      "price": "80000000000000000000",
      "deadline": "2022-08-10T15:16:22.000Z",
      "bidder": "0x585f4fBe2d2A889c286fa71FB81D01f30773F4B1",
      "bidId": "1838102220161507163"
    },
    ...
  }
}
```

### GET `/market/collections/:slug/last-sales`
Returns a list of the most recent sales for a single collection.

#### Request Parameters
| Name   | Type     | Parameter Type | Required? | Description                                                                                      |
| ------ | -------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug` | `string` | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/cryptoadz/last-sales
```

#### Example Response
```json
[
  {
    "tokenId": "396324188277571717",
    "saleTime": "2021-10-05T03:09:51.000Z",
    "priceWei": "25000000000000000000"
  },
  {
    "tokenId": "396324188277584310",
    "saleTime": "2021-09-10T04:08:16.000Z",
    "priceWei": "1000000000000000000"
  },
  {
    "tokenId": "396324188277590271",
    "saleTime": "2022-01-12T00:55:02.000Z",
    "priceWei": "4500000000000000000"
  },
  {
    "tokenId": "396324188277595182",
    "saleTime": "2022-05-13T15:25:25.000Z",
    "priceWei": "2450000000000000000"
  },
  ...
]
```

### GET `/market/collections/:slug/events`
Returns a paginated list of events that took place for a given collection starting from a specific point in time. The `type` query parameter can also be optionally included to filter the response to only include events of the given type. If no `type` parameter is specified, all events after the specified time are included.

Responses include two parameters relevant for paginating through the results:
- `hasNextPage: true | false` - this boolean indicates if there are more pages to get
- `endCursor: {cursorValue}` - pass this cursor in as the `after` query parameter in any follow-up requests to paginate through a set of results

These are the same events that can also be attained using the [WebSocket API](#WebSocket-API). Please reference that section for detailed information on each event/message type.

#### Request Parameters
| Name    | Type     | Parameter Type | Required? | Description                                                                                                                                                                                                                                                           |
| ------- | -------- | -------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `slug`  | `string` | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes                                                                                                                                                                                         |
| `from`  | `string` | `query`        | Yes       | The ISO-8601 formatted datetime string to search starting from. Any event that occured after this time will be returned.                                                                                                                                              |
| `limit` | `int`    | `query`        | No        | The number of results to return per page. Defaults to the maximum value of `1000`.                                                                                                                                                                                    |
| `after` | `string` | `query`        | No        | This is required when paginating through results. To retrieve the next page of results, remove the `from` parameter and then set the `after` query param equal to the `endCursor` value of the current page of results.                                               |
| `type`  | `string` | `query`        | No        | An optional filter parameter to only retrieve certain types of events in the call. Allowed type values are: `ASK_PLACED`, `ASK_CANCELLED`, `BID_PLACED`, `BID_CANCELLED`, `TOKEN_TRADED`, `TOKEN_TRANSFERRED`, `TOKEN_MINTED`, `TRAITS_UPDATED`, and `IMAGES_UPDATED` |

#### Example Paginated Request
Execute the first request with `limit` and `from` set, plus optionally include a `type` filter.

```bash
curl --request GET \
  --url 'https://api.archipelago.art/v1/market/collections/alan-ki-aankhen/events?limit=2&from=2022-08-03'
```

#### Example Response Page 1
Notice that `hasNextPage` is equal to `true` in the response, indicating there is more data to be retrieved.

```json
{
  "events": [
    {
      "messageId": "e0092ea5-eac8-15b1-7fc9-aef84186e0d8",
      "timestamp": "2022-08-03T01:19:13.646Z",
      "type": "BID_CANCELLED",
      "topic": "alan-ki-aankhen",
      "data": {
        "slug": "alan-ki-aankhen",
        "bidId": "1838025065067200105",
        "projectId": "685063080690564926"
      }
    },
    {
      "messageId": "83237faa-35d1-5b37-c314-96eaf4910ad1",
      "timestamp": "2022-08-03T01:36:52.446Z",
      "type": "TOKEN_TRANSFERRED",
      "topic": "alan-ki-aankhen",
      "data": {
        "slug": "alan-ki-aankhen",
        "tokenId": "396950838748550011",
        "logIndex": 236,
        "blockHash": "0x82e20082640f585280667a48f08e01a3fa4f14eefce9d9103a4724e5ff3481a8",
        "toAddress": "0x9774A31B94f97963F776643B2F6690F9617DE279",
        "tokenIndex": 59,
        "blockNumber": 15266625,
        "fromAddress": "0x8605D71d8f494A96345717399D6AdBB28feee295",
        "blockTimestamp": "2022-08-03T01:36:25.000Z",
        "transactionHash": "0x380d9a5af098054fc1dfdf1c6c517fd66a70cbd830219184382d6fffc550e118"
      }
    }
  ],
  "hasNextPage": true,
  "endCursor": "YXItdjEtY29sbGVjdGlvbkV2ZW50c1YxLVsiYWxhbi1raS1hYW5raGVuIixudWxsLCI4MzIzN2ZhYS0zNWQxLTViMzctYzMxNC05NmVhZjQ5MTBhZDEiXQ=="
}
```

#### Example Request 2
Execute a follow-up call to revtreive the next page of data. Repeat this process until `hasNextPage` is `false`, at which point all data will have been returned for the initial query. The follow-up request must be constructed as follows:
- save the value of `hasNextPage` from the first page of results
- make another call to this same endpoint
- remove the `from` query parameter that was included in the first request
- add the `after` query parameter, and set that to the value of `hasNextPage` from the first step
- if a `type` parameter was included in the original request, continue to populate that in each follow-up call as well
- also continue to specify the `limit` query parameter in each follow-up request

Example:
```bash
curl --request GET \
  --url 'https://api.archipelago.art/v1/market/collections/alan-ki-aankhen/events?limit=2&after=YXItdjEtY29sbGVjdGlvbkV2ZW50c1YxLVsiYWxhbi1raS1hYW5raGVuIixudWxsLCI4MzIzN2ZhYS0zNWQxLTViMzctYzMxNC05NmVhZjQ5MTBhZDEiXQ%3D%3D'
```

#### Example Response Page 2
```json
{
  "events": [
    {
      "messageId": "828af0ef-ab62-e8a1-3bfd-216b1d990884",
      "timestamp": "2022-08-03T02:02:37.221Z",
      "type": "TOKEN_TRANSFERRED",
      "topic": "alan-ki-aankhen",
      "data": {
        "slug": "alan-ki-aankhen",
        "tokenId": "396950840989112459",
        "logIndex": 135,
        "blockHash": "0xba7a5e86ee34f8a26b1c6dda715613d4ce0f701a79ce74d8a5a5479a291bd917",
        "toAddress": "0xB97c5725c29f96Daaf8952B051564ACf7F9fB626",
        "tokenIndex": 226,
        "blockNumber": 15266742,
        "fromAddress": "0x9Bc910f14B0EE83689B9F49337B1dfD2962dBB94",
        "blockTimestamp": "2022-08-03T02:02:18.000Z",
        "transactionHash": "0x767c1bcdb3e7b4e043e9a49c053f6df5a527c0dc63dd7b3ebe29fe087934da5c"
      }
    },
    {
      "messageId": "ac162526-fba6-7633-d6da-f202ef4534eb",
      "timestamp": "2022-08-03T03:02:23.247Z",
      "type": "TOKEN_TRANSFERRED",
      "topic": "alan-ki-aankhen",
      "data": {
        "slug": "alan-ki-aankhen",
        "tokenId": "396950842797870421",
        "logIndex": 116,
        "blockHash": "0xb31a77a18bbbc8c2e6389218936eec4c7202e0799bc4e21bb2f1dc9c81b0475d",
        "toAddress": "0x424C51d3E60C043166734C14BACB00fdD24e555a",
        "tokenIndex": 486,
        "blockNumber": 15266963,
        "fromAddress": "0x55613827cE552288142Ea9A738461285309225Cb",
        "blockTimestamp": "2022-08-03T03:01:57.000Z",
        "transactionHash": "0x17a4fab3512d6ee9ac29adc4aab735b2d6a5384a84e6c156203a905a8cf17a42"
      }
    }
  ],
  "hasNextPage": false,
  "endCursor": "YXItdjEtY29sbGVjdGlvbkV2ZW50c1YxLVsiYWxhbi1raS1hYW5raGVuIixudWxsLCJhYzE2MjUyNi1mYmE2LTc2MzMtZDZkYS1mMjAyZWY0NTM0ZWIiXQ=="
}
```


## :art: Token Routes 
The Token routes are a sub-section of the broader Collections routes and enable retrieval of information about individual tokens.

### GET `/market/collections/:slug/:tokenIndex`
Returns the details for a single token (as a `TokenInfo` object) in a collection.

#### Request Parameters
| Name         | Type      | Parameter Type | Required? | Description                                                                                      |
| ------------ | --------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug`       | `string`  | `path`   | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |
| `tokenIndex` | `integer` | `path`   | Yes       | The specific token index within the collection to retrieve.                                      |

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/subscapes/99
```

#### Example Response
```json
{
  "tokenId": "395685417799563123",
  "collectionInfo": {
    "projectId": "683915793512745099",
    "slug": "subscapes",
    "artblocksProjectIndex": 53,
    "imageUrlTemplate": "https://img.archipelago.art/artblocks/{sz}/53/{hi}/{lo}",
    "name": "Subscapes",
    "artistName": "Matt DesLauriers",
    "description": "A generative algorithm that draws the impression of a landscape from a multitude of possibilities. The unique seed from each token drives the parametric assortment of lines, colors, and forms into a constructed composition.",
    "aspectRatio": 1,
    "numTokens": 650,
    "maxInvocations": 650,
    "tokenContract": "0xa7d8d9ef8D8Ce8992Df33D8b8CF4Aebabd5bD270",
    "fees": [
      {
        "target": "0x1212121212121212121212121212121212121212",
        "micros": 5000,
        "static": true
      },
      {
        "target": "0x3434343434343434343434343434343434343434",
        "micros": 5000,
        "static": true
      },
      {
        "target": "0x5656565656565656565656565656565656565656",
        "micros": 75000,
        "static": false
      }
    ]
  },
  "features": [
    {
      "featureId": "972146174609792341",
      "name": "Style",
      "traitId": "1260376550778606275",
      "value": "Pencil",
      "featureSlug": "style",
      "traitSlug": "pencil"
    },
    {
      "featureId": "972146174609792940",
      "name": "Patchwork",
      "traitId": "1260376550778635632",
      "value": "True",
      "featureSlug": "patchwork",
      "traitSlug": "true"
    },
    ...
  ],
  "history": [
    {
      "type": "TRANSFER",
      "blockNumber": 12297717,
      "logIndex": 101,
      "transactionHash": "0x454db245ea1ee8192931436801275095c5ddd54db7a2e628d281747e2b27c31f",
      "blockHash": "0xf2f224971c900b69edceec7d0ed371b02a75402a0fe790a0b60eaefb68e00b5c",
      "timestamp": "2021-04-23T17:01:44.000Z",
      "from": "0x0000000000000000000000000000000000000000",
      "to": "0xb63a5C5710F06e111fa14AC82dA2183C5102B504"
    },
    ...
  ],
  "currentOwner": "0x0F0eAE91990140C560D4156DB4f00c854Dc8F09E",
  "chainData": {
    "tokenContract": "0xa7d8d9ef8D8Ce8992Df33D8b8CF4Aebabd5bD270",
    "onChainTokenId": "53000099"
  },
  "asks": {
    "top": [],
    "more": false
  },
  "bids": {
    "top": [],
    "more": false
  }
}
```

### GET `/market/collections/:slug/:tokenIndex/features`
Returns the features and traits (as a list of `TokenTrait` objects) for a single token in a collection.

#### Request Parameters
| Name         | Type      | Parameter Type | Required? | Description                                                                                      |
| ------------ | --------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug`       | `string`  | `path`    | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |
| `tokenIndex` | `integer` | `path`    | Yes       | The specific token index within the collection to retrieve.                                      |

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/subscapes/99/features
```

#### Example Response
```json
[
  {
    "featureId": "972146174609792341",
    "name": "Style",
    "traitId": "1260376550778606275",
    "value": "Pencil",
    "featureSlug": "style",
    "traitSlug": "pencil"
  },
  {
    "featureId": "972146174609792940",
    "name": "Patchwork",
    "traitId": "1260376550778635632",
    "value": "True",
    "featureSlug": "patchwork",
    "traitSlug": "true"
  },
  {
    "featureId": "972146174609793564",
    "name": "Lattice",
    "traitId": "1260376550778654067",
    "value": "False",
    "featureSlug": "lattice",
    "traitSlug": "false"
  },
  ...
]
```

### GET `/market/collections/:slug/:tokenIndex/history`
Returns the trade and transfer history (as a list of `TokenHistory` objects) for a single token in a collection.

#### Parameters
| Name         | Type      | Required? | Description                                                                                      |
| ------------ | --------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug`       | `string`  | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |
| `tokenIndex` | `integer` | Yes       | The specific token index within the collection to retrieve.

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/fidenza/1/history
```

#### Example Response
```json
[
  {
    "type": "TRANSFER",
    "blockNumber": 12614178,
    "logIndex": 113,
    "transactionHash": "0xb01287ebc4744ec00270f119f5a1ec79b349261c87d04c8d915c1065a284d726",
    "blockHash": "0xb993a4ea3d2f44ae391d465e90a1d204708eed2c51d3e7445bedf9f43a2860af",
    "timestamp": "2021-06-11T15:59:46.000Z",
    "from": "0x0000000000000000000000000000000000000000",
    "to": "0x98855508E8D8D307dEd4aEB38014b87D236Da2Ba"
  },
  ...
  {
    "type": "OPENSEA_SALE",
    "from": "0x8f1BB5C9Ed94341C4274bc6B66c2B8978Ed2c2C1",
    "to": "0x88e38E2134Ac4164187Cc7CdfED24afA8726789a",
    "timestamp": "2021-09-09T02:33:59.000Z",
    "transactionHash": "0xb492783c3fe37f3ad0f5931811c9c85d570617b8cc0c57698093046b36b40c89",
    "priceWei": "205000000000000000000"
  }
  ...
}
```

### GET `/market/collections/:slug/:tokenIndex/ask`
Returns the ask (price, in WEI) for a single token in a collection.

#### Request Parameters
| Name         | Type      | Parameter Type | Required? | Description                                                                                      |
| ------------ | --------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug`       | `string`  | `path` | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |
| `tokenIndex` | `integer` | `path` | Yes       | The specific token index within the collection to retrieve. 

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/cryptoadz/6/ask
```

#### Example Response
```json
{
  "collection": "edifice",
  "tokenIndex": "676",
  "tokenId": "395685422042547544",
  "ask": {
    "asker": "0x47d8404fCD1c52E6642C7eD374FaB052b381Ccc1",
    "askId": "opensea:7029748975",
    "price": "49000000000000000000",
    "createTime": "2022-06-28T21:31:51.000Z",
    "deadline": "2022-09-08T13:44:43.000Z",
    "tokenId": "395685422042547544",
    "venue": "OPENSEA"
  }
}
```

### GET `/market/collections/:slug/:tokenIndex/orders`
Returns the active bids and asks (price, in WEI) for a single token in a collection.

#### Request Parameters
| Name         | Type      | Parameter Type | Required? | Description                                                                                      |
| ------------ | --------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug`       | `string`  | `path` | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |
| `tokenIndex` | `integer` | `path` | Yes       | The specific token index within the collection to retrieve. 

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/chromie-squiggle/335/orders
```

#### Example Response
```json
{
  "bids": [
    {
      "bidId": "1838056026246931030",
      "slug": "chromie-squiggle",
      "name": "Chromie Squiggle",
      "price": "20000000000000000",
      "deadline": "2022-08-02T11:28:38.000Z",
      "bidder": "0x2CFAe7706ADf3333512016365C2E4f95F6cBe7B2",
      "nonce": "1658230118347",
      "signatureData": {
        "message": "0x00000000000000000000000000000000000000000000000000000000000000207a3965c2c468a8fb3f1687ed769b8ade5463c5905fbb0b92a9bf34aebf32780500000000000000000000000000000000000000000000000000000182163797cb0000000000000000000000000000000000000000000000000000000062e90a6600000000000000000000000000000000000000000000000000000000000000c000000000000000000000000000000000000000000000000000000000000000e0000000000000000000000000a6ae1c1dc3024ec951972a10a7043bc7425f1f570000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002046700b4d40ac5c35af2c22dda2787a91eb567b06c924a8fb8ae9a05b20c08c00",
        "signature": "0xf3810b1c6318fc77226f2573d521021964a9ce8d4c50fc1e9470e194c6e7d5f84308236bdacf59f868c0f039a2e90645472fcf379d7b1e81bcd09f5a4241acb81b",
        "agreement": "0x0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc200000000000000000000000000000000000000000000000000470de4df820000000000000000000000000000059edd72cd353df5106d2b9cc5ab83a52287ac3a00000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000002a76456bb6abc50fb38e17c042026bc27a95c33140000000000000000800013888a3f65ef24021d401815792c4b65676fbf90663c00000000000061a8000124f8"
      },
      "scope": {
        "type": "PROJECT",
        "scope": "683915793512607080"
      }
    },
    ...
  ],
  "asks": [
    {
      "asker": "0x80fb5880F38185661962E475ac1557817dc9faea",
      "askId": "opensea:7221908994",
      "price": "10400000000000000000",
      "createTime": "2022-07-27T19:21:39.000Z",
      "deadline": "2022-08-27T19:21:39.000Z",
      "tokenId": "395685417410643656",
      "venue": "OPENSEA"
    }
  ]
}
```


## :female-office-worker: User Routes
The user routes contain endpoints to register, login, and manage all user functions.


### POST `/user/login`
:construction: Coming soon!

### POST `/user/set-email` :lock:
Updates the email address that is associated to the user. This will trigger an email to be sent to that email address to confirm the change. Confirmation should only be done via the link in the email.


#### Example Request
```bash
curl --request POST \
  --url https://api.archipelago.art/v1/user/set-email \
  --header 'Content-Type: application/json' \
  --header 'x-archipelago-frontend-token: [YOUR API TOKEN]' \
  --data '{
  "email": "email@test.com"
}'
```

#### Example Response
```json
{
  "email": "email@test.com"
}
```

### GET `/user/info` :lock: 
Returns basic user information (as a `UserInfo` object) for the authenticated user.

#### Example Request
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/user/info \
  --header 'x-archipelago-frontend-token: [YOUR API TOKEN]'
```

#### Example Response
```json
{
  "user": {
    "account": "0x6959B455A5514a778Acd673Fc7e9cDD4429dB5e5",
    "email": null,
    "preferences": null
  }
}
```

### GET `/user/bids` :lock:
Returns a list of active bids for the authenticated user.

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/user/bids \
  --header 'x-archipelago-frontend-token: [YOUR API TOKEN]'
```

#### Example Response
```json
{
  "bids": [
    {
      "bidId": "1838104330282441408",
      "slug": "freehand",
      "name": "Freehand",
      "price": "100000000000000000",
      "deadline": "2022-08-11T00:13:00.000Z",
      "bidder": "0x6959B455A5514a778Acd673Fc7e9cDD4429dB5e5",
      "nonce": "1658967180807",
      "signatureData": {
        "message": "0x000000000000000000000000000000000000000000000000000000000000002029f96153dcd42c7cc8df29df98d239f396ee4b5bad66b08ce5e7a60825d2329000000000000000000000000000000000000000000000000000000182422646070000000000000000000000000000000000000000000000000000000062f4498c00000000000000000000000000000000000000000000000000000000000000c000000000000000000000000000000000000000000000000000000000000000e0000000000000000000000000a6ae1c1dc3024ec951972a10a7043bc7425f1f57000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000209ba4a2096bc1848b8e7cbd0f5e4b7e15dfcb45fd9ccf34b3ec2bab64154f0800",
        "signature": "0x1fcec9fb941dcca038929bcc3997f0980b65b3be62739088ff12b646c9de27f70efffd7a4b42b3d1af731facf5fe5b24de5adbc25ad05349deff1a01e27723361b",
        "agreement": "0x0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2000000000000000000000000000000000000000000000000016345785d8a0000000000000000000000000000a7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd27000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000002a76456bb6abc50fb38e17c042026bc27a95c33140000000000000000800013888a3f65ef24021d401815792c4b65676fbf90663c00000000000061a8000124f8"
      },
      "scope": {
        "type": "PROJECT",
        "slug": "freehand",
        "name": "Freehand"
      }
    },
    ...
  ]
}
```

### GET `/user/asks` :lock:
Returns a list of active sales for the authenticated user.

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/user/asks \
  --header 'x-archipelago-frontend-token: [YOUR API TOKEN]'
```

#### Example Response
```json
{
  "asks": [
    {
      "askId": "2126261679923620167",
      "slug": "freehand",
      "name": "Freehand",
      "price": "700000000000000000",
      "createTime": "2022-07-15T02:41:27.928Z",
      "deadline": "2022-07-29T02:41:23.000Z",
      "asker": "0x1E21073744fa7Fadb9D19150CE0E23d37d97e728",
      "nonce": "1657852883953",
      "tokenId": "395685422044438988",
      "tokenIndex": 66,
      "signatureData": {
        "message": "0x000000000000000000000000000000000000000000000000000000000000002075a5f47b913262db048f017665d36d2740b0d1dcbe7e300406d8599e14935aab00000000000000000000000000000000000000000000000000000181ffbb73f10000000000000000000000000000000000000000000000000000000062e348d300000000000000000000000000000000000000000000000000000000000000e0000000000000000000000000000000000000000000000000000000000c939b02000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
        "signature": "0x26153afb0282261c53e915d629d913fff04c3e83332dcfffae1b29fa5eb63b352b23176fe662d83ce0b284655d693776c526046917e67f37ee1f487766441a951c",
        "agreement": "0x0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc200000000000000000000000000000000000000000000000009b6e64a8ec60000000000000000000000000000a7d8d9ef8d8ce8992df33d8b8cf4aebabd5bd27000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000002a76456bb6abc50fb38e17c042026bc27a95c33140000000000000000800013888a3f65ef24021d401815792c4b65676fbf90663c00000000000061a8000124f8"
      }
    },
    ...
  ]
}
```

### GET `/user/:account/tokens` :lock:
```bash
curl --request GET \
  --url https://api.archipelago.art/v1/user/info \
  --header 'x-archipelago-frontend-token: [YOUR API TOKEN]'
```

#### Example Response
```json
{
  "tokens": [
    {
      "name": "Freehand",
      "slug": "freehand",
      "imageUrlTemplate": "https://img.archipelago.art/artblocks/{sz}/211/000/066",
      "tokenIndex": 66,
      "tokenId": "395685422044438988",
      "artistName": "WAWAA",
      "aspectRatio": 1,
      "tokenContract": "0xa7d8d9ef8D8Ce8992Df33D8b8CF4Aebabd5bD270",
      "onChainTokenId": "211000066",
      "bid": null
    }
  ]
}
```


# WebSocket API
It's also possible to communicate with the Archipelago API via a WebSocket connection. WebSockets are best suited for clients and applications that need real-time data. The Archipelago WebSocket server allows clients to subscribe to a feed of events for one or many `collections`.

## Message Pairs
These are the pairs of message that you (as the client) will send and receive when establishing a connection to the Archipelago WebSocket and subscribing to different topics.

### Heartbeat
#### Example Request
```json
{
  "type": "HEARTBEAT"
}
```

#### Example Response
```json
{
  "type": "HEARTBEAT_RESPONSE", 
  "data": {
    "time":1655056473
  },
  "status":200
}
```

### Subscribe Topic
#### Example Request
```json
{
  "type": "SUBSCRIBE_TOPIC",
  "topic": "ringers"
}
```

#### Example Response
```json
{
  "type": "ADD_TOPIC",
  "data": {
    "topics": [
      "ringers"
    ]
  },
  "status": 200
}
```

### Unsubscribe Topic
#### Example Request
```json
{
  "type": "UNSUBSCRIBE_TOPIC",
  "topic": "ringers"
}
```

#### Example Response
```json
{
  "type": "REMOVE_TOPIC",
  "data":{
    "topics": []
  },
  "status": 200
}
```

## Message Types
These are the different types of messages that you can expect to receive once subscribed to a topic on the Archipelago WebSocket.

### Token Transferred
#### Example Message
```json
{
  "messageId": "5f93d16a-9baf-abb8-de44-e7a96aaa04df",
  "timestamp": "2022-07-08T19:51:56.929Z",
  "type": "TOKEN_TRANSFERRED",
  "topic": "rapture",
  "data": {
    "slug": "rapture",
    "tokenId": "395685420569574938",
    "logIndex": 668,
    "blockHash": "0xfe85a10a0e613360b122bbbe45c3785d45eedec6aaf5487cc7dd2f78ea542ba6",
    "toAddress": "0x4Dd5A4D1fcb6F8938aa8AD070aEFE1B19e8F9c0C",
    "tokenIndex": 79,
    "blockNumber": 15103957,
    "fromAddress": "0xdDcC629c76F311d894b7c2953942A8652Df2985d",
    "blockTimestamp": "2022-07-08T19:51:47.000Z",
    "transactionHash": "0x2dad95e4378a0b015ad92546c1ba745c2d96c3fce8a1699d9e4d312bb892b0e2"
  }
}
```

### Token Traded
#### Example Message
```json
{
  "messageId": "71ea8668-1474-c477-70d7-df12756240f0",
  "timestamp": "2022-07-09T06:37:29.284Z",
  "type": "TOKEN_TRADED",
  "topic": "rapture",
  "data": {
    "cost": "600000000000000000",
    "slug": "rapture",
    "buyer": "0x42eeD6182E4f3E37D3aE08a0d2A04C258ee0aE87",
    "price": "600000000000000000",
    "seller": "0x73e60cD967E957bC6e074F93320FfA1d52697D5b",
    "tokenId": "395685420569582837",
    "tradeId": "0x462cba9d7065a2ad72db2a9ef2806e260a5614e6fdeceefdf57b29452f8885ba",
    "currency": "0xC02aaA39b223FE8D0A0e5C4F27eAD9083C756Cc2",
    "logIndex": 149,
    "proceeds": "549000000000000000",
    "blockHash": "0xee0436b8b85c194cbb2fdf380279d460cb03999990783e53340480f1d72d5ab7",
    "tokenIndex": 154,
    "blockNumber": 15106784,
    "blockTimestamp": "2022-07-09T06:37:22.000Z",
    "transactionHash": "0x1d14c14bcff14c149ab74abb6a828d8ba74a24198f01e39a9806edae40764634"
  }
}
```

### Token Minted
#### Example Message
```json
{
  "messageId": "daa6a459-09e0-9974-10e8-3192ccd8bc35",
  "timestamp": "2022-10-18T19:13:28.627Z",
  "type": "TOKEN_MINTED",
  "topic": "ALL_COLLECTIONS",
  "data": {
    "slug": "orchids",
    "tokenId": "397421243270088858",
    "projectId": "685616547712419862",
    "tokenIndex": 61,
    "tokenContract": "0x0A1BBD57033F57E7B6743621b79fCB9Eb2CE3676",
    "onChainTokenId": 16000061
  }
}
```

### Bid Placed
#### Example Message
```json
{
  "messageId": "ba4d7f4f-bc68-7f07-46cb-bfe7f8946b9a",
  "timestamp": "2022-07-09T11:45:24.539Z",
  "type": "BID_PLACED",
  "topic": "rapture",
  "data": {
    "slug": "rapture",
    "bidId": "1837938281097037349",
    "nonce": "1656433465713",
    "price": "250000000000000000",
    "scope": {
      "slug": "rapture",
      "type": "PROJECT",
      "projectId": "683915793512728635"
    },
    "venue": "ARCHIPELAGO",
    "bidder": "0x8bD9C4B5eA8F6f14c9B14d830ddb67f3720d77F6",
    "currency": "ETH",
    "projectId": "683915793512728635",
    "timestamp": "2022-06-28T16:24:34.442Z",
    "expirationTime": "2022-07-12T16:24:25.000Z"
  }
}
```

### Bid Cancelled
#### Example Message
```json
{
  "messageId": "aa9852d4-2dbd-2579-1473-d7ca9b0c3c52",
  "timestamp": "2022-07-08T21:21:37.711Z",
  "type": "BID_CANCELLED",
  "topic": "rapture",
  "data": {
    "slug": "rapture",
    "bidId": "1837938281097037349",
    "projectId": "683915793512728635"
  }
}
```

### Ask Placed
#### Example Message
```json
{
  "messageId": "72831719-9684-a96c-a884-ec20bc17e67e",
  "timestamp": "2022-07-08T21:56:55.477Z",
  "type": "ASK_PLACED",
  "topic": "rapture",
  "data": {
    "slug": "rapture",
    "askId": "opensea:7103384369",
    "price": "890000000000000000",
    "venue": "OPENSEA",
    "seller": "0x73e60cD967E957bC6e074F93320FfA1d52697D5b",
    "tokenId": "395685420569582837",
    "currency": "ETH",
    "projectId": "683915793512728635",
    "timestamp": "2022-07-08T21:24:17.000Z",
    "tokenIndex": 154,
    "expirationTime": "2022-08-08T21:24:17.000Z"
  }
}
```

### Ask Cancelled
#### Example Message
```json
{
  "messageId": "c3478bae-e4f6-9f02-19fe-b8eb7dd788fb",
  "timestamp": "2022-07-09T06:37:27.957Z",
  "type": "ASK_CANCELLED",
  "topic": "rapture",
  "data": {
    "slug": "rapture",
    "askId": "2126207238801129012",
    "projectId": "683915793512728635",
    "tokenIndex": 154
  }
}
```

### Traits Updated
#### Example Message
```json
{
  "messageId": "7e0df5cf-cd19-f79e-58ca-d781e9ddc003",
  "timestamp": "2022-07-27T17:31:08.055Z",
  "type": "TRAITS_UPDATED",
  "topic": "alan-ki-aankhen",
  "data": {
    "slug": "alan-ki-aankhen",
    "traits": [
      {
        "traitId": "1261641997534706964",
        "featureId": "973293462407744960",
        "traitSlug": "medium",
        "traitValue": "medium",
        "featureName": "pen",
        "featureSlug": "pen"
      },
      {
        "traitId": "1261641997534710972",
        "featureId": "973293462407757230",
        "traitSlug": "spirals",
        "traitValue": "spirals",
        "featureName": "sky",
        "featureSlug": "sky"
      },
      {
        "traitId": "1261523838559801602",
        "featureId": "973293462407763655",
        "traitSlug": "night",
        "traitValue": "night",
        "featureName": "time",
        "featureSlug": "time"
      },
      {
        "traitId": "1261641997534728108",
        "featureId": "973293462407781532",
        "traitSlug": "smoke",
        "traitValue": "smoke",
        "featureName": "paper",
        "featureSlug": "paper"
      },
      {
        "traitId": "1261641997534737191",
        "featureId": "973293462407793930",
        "traitSlug": "regular",
        "traitValue": "regular",
        "featureName": "moon size",
        "featureSlug": "moon-size"
      },
      {
        "traitId": "1261641997534742313",
        "featureId": "973293462407796266",
        "traitSlug": "eyescape",
        "traitValue": "eyescape",
        "featureName": "composition",
        "featureSlug": "composition"
      },
      {
        "traitId": "1261641997534752394",
        "featureId": "973293462407804782",
        "traitSlug": "1",
        "traitValue": "1",
        "featureName": "number of moons",
        "featureSlug": "number-of-moons"
      }
    ],
    "tokenId": "396950834593777974",
    "projectId": "685063080690564926",
    "tokenIndex": 14
  }
}
```

### Images Updated
#### Example Message
```json
{
  "messageId": "fa670647-5c88-3bd8-b0d2-37cbd68910c9",
  "timestamp": "2022-07-27T17:20:31.498Z",
  "type": "IMAGES_UPDATED",
  "topic": "alan-ki-aankhen",
  "data": {
    "slug": "alan-ki-aankhen",
    "tokenId": "396950822729822707",
    "projectId": "685063080690564926",
    "tokenIndex": 1,
    "tokenContract": "0xa7d8d9ef8D8Ce8992Df33D8b8CF4Aebabd5bD270",
    "onChainTokenId": "333000001"
  }
}
```

## Message Nonce
Any message that you send may include an optional `nonce` field. If specified, the server will return it back to you in the response message. This can be useful if you want to track the reponse to individual messages admist a large amount of traffic. An example of this can be found in the sample code below.

## Sample Code
The code below provides a simplified example of how to connect to the Archipelago WebSocket API to send and receive your first messages.

The sample code below is written in [vanilla JavaScript](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_client_applications) designed to run in the browser.

```javascript
// Define the WebSocket and open the connection
let socket = new WebSocket("wss://api.archipelago.art/ws");

// Handle the connection open event
socket.onopen = function(event) {
  console.log("Connection to Archipelago WS established.");

  // Send an initial heartbeat message
  var heartbeat_msg = {type: "HEARTBEAT"};
  socket.send(JSON.stringify(heartbeat_msg));

  // Subscribe to receive events for a collection
  var subscribe_msg = { nonce: Date.now(), type: "SUBSCRIBE_TOPIC", topic: "ringers" };
  socket.send(JSON.stringify(subscribe_msg));
}

// Listen for messages back from the Archipelago API
socket.onmessage = function(event) {
  console.log(`Data received from Archipelago WS: ${event.data}`);
};

// Handle any errors
socket.onerror = function(error) {
  console.error(`Error ${error.message}`);
};

// Handle closing the connection
socket.onclose = function(event) {
  if (event.wasClean) {
    console.log(`Connection closed cleanly, code=${event.code} reason=${event.reason}`);
  } else {
    // e.g. server process killed or network down
    // event.code is usually 1006 in this case
    console.error(`Connection died, code=${event.code}`);
  }
};
```

### Sample Output
Running the sample code above should yield the output below:
```
Connection to Archipelago WS established.
Data received from Archipelago WS: {"type":"HEARTBEAT_RESPONSE","data":{"time":1655056473},"status":200}
Data received from Archipelago WS: {"type":"ADD_TOPIC","data":{"topics":["ringers"]},"status":200,"nonce":1655069434775}
```