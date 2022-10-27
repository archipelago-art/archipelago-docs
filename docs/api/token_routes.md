---
layout: default
title: Token Routes
parent: API Routes
nav_order: 4
---

# :art: Token Routes

The Token routes are a sub-section of the broader Collections routes and enable retrieval of information about individual tokens.

## GET `/market/collections/:slug/:tokenIndex`

Returns the details for a single token (as a `TokenInfo` object) in a collection.

### Request Parameters

| Name         | Type      | Parameter Type | Required? | Description                                                                                      |
| ------------ | --------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug`       | `string`  | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |
| `tokenIndex` | `integer` | `path`         | Yes       | The specific token index within the collection to retrieve.                                      |

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/subscapes/99
```

### Example Response

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

## GET `/market/collections/:slug/:tokenIndex/features`

Returns the features and traits (as a list of `TokenTrait` objects) for a single token in a collection.

### Request Parameters

| Name         | Type      | Parameter Type | Required? | Description                                                                                      |
| ------------ | --------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug`       | `string`  | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |
| `tokenIndex` | `integer` | `path`         | Yes       | The specific token index within the collection to retrieve.                                      |

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/subscapes/99/features
```

### Example Response

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

## GET `/market/collections/:slug/:tokenIndex/history`

Returns the trade and transfer history (as a list of `TokenHistory` objects) for a single token in a collection.

### Parameters

| Name         | Type      | Required? | Description                                                                                      |
| ------------ | --------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug`       | `string`  | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |
| `tokenIndex` | `integer` | Yes       | The specific token index within the collection to retrieve.                                      |

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/fidenza/1/history
```

### Example Response

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

## GET `/market/collections/:slug/:tokenIndex/ask`

Returns the ask (price, in WEI) for a single token in a collection.

### Request Parameters

| Name         | Type      | Parameter Type | Required? | Description                                                                                      |
| ------------ | --------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug`       | `string`  | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |
| `tokenIndex` | `integer` | `path`         | Yes       | The specific token index within the collection to retrieve.                                      |

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/cryptoadz/6/ask
```

### Example Response

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

## GET `/market/collections/:slug/:tokenIndex/orders`

Returns the active bids and asks (price, in WEI) for a single token in a collection.

### Request Parameters

| Name         | Type      | Parameter Type | Required? | Description                                                                                      |
| ------------ | --------- | -------------- | --------- | ------------------------------------------------------------------------------------------------ |
| `slug`       | `string`  | `path`         | Yes       | The unique slug of the collection. This will be all lowercase and have dashes instead of spaces. |
| `tokenIndex` | `integer` | `path`         | Yes       | The specific token index within the collection to retrieve.                                      |

### Example Request

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/market/collections/chromie-squiggle/335/orders
```

### Example Response

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
