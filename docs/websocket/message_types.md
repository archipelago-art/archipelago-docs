---
layout: default
title: Message Types
parent: WebSocket API
nav_order: 2
---

# 📒 WebSocket Message Types
{: .no_toc }

These are the different types of messages that you can expect to receive once subscribed to a topic on the Archipelago WebSocket.

## Table of Contents
{: .no_toc .text-delta }
- TOC
{:toc}

---

## Token Transferred

### Example Message
{: .no_toc }

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

## Token Traded

### Example Message
{: .no_toc }

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

## Token Minted

### Example Message
{: .no_toc }

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

## Bid Placed

### Example Message
{: .no_toc }

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

## Bid Cancelled

### Example Message
{: .no_toc }

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

## Ask Placed

### Example Message
{: .no_toc }

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

## Ask Cancelled

### Example Message
{: .no_toc }

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

## Traits Updated

### Example Message
{: .no_toc }

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

## Images Updated

### Example Message
{: .no_toc }

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