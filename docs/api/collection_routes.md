---
layout: default
title: Collection Routes
parent: API Routes
nav_order: 3
---

# :art: Collections Routes

The collections routes contain endpoints to retrieve information about collections and the tokens within them.

## GET `/market/collections`

Returns a list of top-level information (as `CollectionInfo` objects) for all Archipelago supported collections.

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections
```

### Example Response

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

## GET `/market/collections/:slug`

Returns the top-level details (as a `CollectionInfo` object) of a single collection, as well as a list of the tokens (as `CollectionToken` objects) in the collection.

### Request Parameters

| Name   | Type     | Parameter Type | Required? | Description                                                                                      |
| ------ | -------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug` | `string` | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/ringers
```

### Example Response

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

## GET `/market/collections/:slug/features`

Returns the features and traits of a single collection (as a `CollectionFeature` object, as well as a list of each token that has a given trait.

### Request Parameters

| Name   | Type     | Parameter Type | Required? | Description                                                                                      |
| ------ | -------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug` | `string` | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/ringers/features
```

### Example Response

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

## GET `/market/collections/:slug/asks`

Returns the lowest ask (price) for each token in a collection that has at least one active ask. They key of the 'asks' object is the `tokenIndex` that the ask is associated to.

### Request Parameters

| Name   | Type     | Parameter Type | Required? | Description                                                                                      |
| ------ | -------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug` | `string` | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/fidenza/asks
```

### Example Response

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

## GET `/market/collections/:slug/bids`

Returns the highest bid for each token in a collection that has at least one active bid. They key of the 'bids' object is the `tokenIndex` that the bid is associated to.

### Request Parameters

| Name   | Type     | Parameter Type | Required? | Description                                                                                      |
| ------ | -------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug` | `string` | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/chromie-squiggle/bids
```

### Example Response

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

## GET `/market/collections/:slug/last-sales`

Returns a list of the most recent sales for a single collection.

### Request Parameters

| Name   | Type     | Parameter Type | Required? | Description                                                                                      |
| ------ | -------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug` | `string` | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/cryptoadz/last-sales
```

### Example Response

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

## GET `/market/collections/:slug/events`

Returns a paginated list of events that took place for a given collection starting from a specific point in time. The `type` query parameter can also be optionally included to filter the response to only include events of the given type. If no `type` parameter is specified, all events after the specified time are included.

Responses include two parameters relevant for paginating through the results:

- `hasNextPage: true | false` - this boolean indicates if there are more pages to get
- `endCursor: {cursorValue}` - pass this cursor in as the `after` query parameter in any follow-up requests to paginate through a set of results

These are the same events that can also be attained using the [WebSocket API](#WebSocket-API). Please reference that section for detailed information on each event/message type.

### Request Parameters

| Name    | Type     | Parameter Type | Required? | Description                                                                                                                                                                                                                                                           |
| ------- | -------- | -------------- | --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `slug`  | `string` | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes                                                                                                                                                                                         |
| `from`  | `string` | `query`        | Yes       | The ISO-8601 formatted datetime string to search starting from. Any event that occured after this time will be returned.                                                                                                                                              |
| `limit` | `int`    | `query`        | No        | The number of results to return per page. Defaults to the maximum value of `1000`.                                                                                                                                                                                    |
| `after` | `string` | `query`        | No        | This is required when paginating through results. To retrieve the next page of results, remove the `from` parameter and then set the `after` query param equal to the `endCursor` value of the current page of results.                                               |
| `type`  | `string` | `query`        | No        | An optional filter parameter to only retrieve certain types of events in the call. Allowed type values are: `ASK_PLACED`, `ASK_CANCELLED`, `BID_PLACED`, `BID_CANCELLED`, `TOKEN_TRADED`, `TOKEN_TRANSFERRED`, `TOKEN_MINTED`, `TRAITS_UPDATED`, and `IMAGES_UPDATED` |

### Example Paginated Request

Execute the first request with `limit` and `from` set, plus optionally include a `type` filter.

```bash
curl --request GET \
  --url 'https://api.archipelago.art/v1/market/collections/alan-ki-aankhen/events?limit=2&from=2022-08-03'
```

### Example Response Page 1

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

### Example Request 2

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

### Example Response Page 2

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
