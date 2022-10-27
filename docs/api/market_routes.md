---
layout: default
title: 📈 Market Routes
parent: API Routes
nav_order: 2
---

# 📈 Market Routes

The base-level market routes contain endpoints to retrieve information about the overall market (views, volume, floors, and more).

## GET `/market/views`

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/views
```

### Example Response

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

## GET `/market/volume`

Returns the market volume (total sales, in WEI) for each collection on the Archipelago marketplace. The required `duration` query parameter determines the period of time that the volume is calculated for.

### Request Parameters

| Name       | Type     | Parameter Type | Required? | Description                                                                   |
| ---------- | -------- | -------------- | --------- | ----------------------------------------------------------------------------- |
| `duration` | `string` | `query`        | Yes       | The duration to lookback. Must be one of the three values: `24h`, `7d`, `30d` |

### Example Request

```bash
curl --request GET \
  --url 'https://api.archipelago.art/v1/market/volume?duration=24h'
```

### Example Response

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

## GET `/market/floor-asks`

Returns the floor ask for each collection.

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/floor-asks
```

### Example Response

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

## GET `/market/floor-bids`

Returns the floor bid (price, in WEI) for each collection. Any floor bid is a `PROJECT` level bid.

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/floor-bids
```

### Example Response

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

## GET `/market/bids/:bidId`

Returns the details of a specific bid.

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/bids/1837909952121726225
```

### Example Response

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

## GET `/market/asks/:ask`

Returns the details of a specific ask

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/asks/2126219693463423900
```

### Example Response

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
