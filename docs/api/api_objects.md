---
layout: default
title: Object Types
parent: REST API
nav_order: 1
last_modified_date: "2022-10-30"
---

# 📦 Object Types
{: .no_toc }

These are the common response types that you will see in the Archipelago REST API.
The documentation for an individual route will likely reference one or more of these objects.

## Table of contents
{: .no_toc .text-delta }
- TOC
{:toc}

---

## Collection Objects

### `CollectionInfo`

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

### `CollectionFees`

| Name     | Type     | Description                            |
| -------- | -------- | -------------------------------------- | ------- |
| `target` | `string` | The target address to send the fee to. |
| `micros` | `string` | The amount of the fee.                 |
| `static` | `string` | A boolean `true                        | false`. |

### `CollectionToken`

| Name         | Type     | Description                                      |
| ------------ | -------- | ------------------------------------------------ |
| `tokenId`    | `string` | The unique id of a token.                        |
| `tokenIndex` | `string` | The unique index of a token within a collection. |

### `CollectionFeature`

| Name        | Type     | Description                          |
| ----------- | -------- | ------------------------------------ |
| `featureId` | `string` | The unique id of the feature.        |
| `name`      | `string` | The name of the feature.             |
| `traits`    | `array`  | A list of `CollectionTrait` objects. |

### `CollectionTrait`

| Name           | Type     | Description                                     |
| -------------- | -------- | ----------------------------------------------- |
| `traitId`      | `string` | The unique id of the trait.                     |
| `value`        | `string` | The value of the trait.                         |
| `tokenIndices` | `array`  | A list of tokenIndices that contain this trait. |
| `slug`         | `string` | The unique slug of the trait.                   |

### `CollectionAsk`

| Name          | Type     | Description                                            |
| ------------- | -------- | ------------------------------------------------------ |
| `priceWei`    | `string` | The asking price (in WEI) for the token.               |
| `listingTime` | `string` | The time the ask was listed.                           |
| `venue`       | `array`  | The venue or marketplace that the ask originated from. |

### `CollectionSale`

| Name       | Type     | Description                               |
| ---------- | -------- | ----------------------------------------- |
| `tokenId`  | `string` | The ID of the token that was sold.        |
| `saleTime` | `string` | The timestamp that the sale was made.     |
| `priceWei` | `array`  | The purchase amount (in WEI) of the sale. |

## Token Objects

### `TokenInfo`

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

### `TokenTrait` 

| Name          | Type     | Description                             |
| ------------- | -------- | --------------------------------------- |
| `featureId`   | `string` | The unique id of the collection.        |
| `name`        | `string` | The unique text slug of the collection. |
| `traitId`     | `array`  | The project index on artblocks.         |
| `value`       | `string` | The project index on artblocks.         |
| `featureSlug` | `string` | The project index on artblocks.         |
| `traitSlug`   | `string` | The project index on artblocks.         |

### `TokenHistory`

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

### `User`

| Name          | Type     | Description                                  |
| ------------- | -------- | -------------------------------------------- |
| `account`     | `string` | The Ethereum address associated to the user. |
| `email`       | `string` | The user's email address.                    |
| `preferences` | `string` | The user's preferences.                      |

### `UserBid`

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

### `BidScope`

| Name         | Type     | Description                                  |
| ------------ | -------- | -------------------------------------------- |
| `type`       | `string` | The Ethereum address associated to the user. |
| `tokenIndex` | `string` | The user's email address.                    |
| `tokenId`    | `string` | The user's preferences.                      |
| `slug`       | `string` | The user's preferences.                      |
| `name`       | `string` | The user's preferences.                      |
