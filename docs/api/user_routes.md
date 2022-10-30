---
layout: default
title: User Routes
parent: REST API
nav_order: 6
---

# 👩‍💼 User Routes
{: .no_toc }

The user routes contain endpoints to register, login, and manage all user functions.

## Table of contents
{: .no_toc .text-delta }
- TOC
{:toc}

---

## POST `/user/login`

🚧 Coming soon!

## POST `/user/set-email` 🔒 

Updates the email address that is associated to the user. This will trigger an email to be sent to that email address to confirm the change. Confirmation should only be done via the link in the email.

### Example Request
{:  .no_toc }

```bash
curl --request POST \
  --url https://api.archipelago.art/v1/user/set-email \
  --header 'Content-Type: application/json' \
  --header 'x-archipelago-frontend-token: [YOUR API TOKEN]' \
  --data '{
  "email": "email@test.com"
}'
```

### Example Response
{:  .no_toc }

```json
{
  "email": "email@test.com"
}
```

## GET `/user/info` 🔒

Returns basic user information (as a `UserInfo` object) for the authenticated user.

### Example Request
{:  .no_toc }

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/user/info \
  --header 'x-archipelago-frontend-token: [YOUR API TOKEN]'
```

### Example Response
{:  .no_toc }

```json
{
  "user": {
    "account": "0x6959B455A5514a778Acd673Fc7e9cDD4429dB5e5",
    "email": null,
    "preferences": null
  }
}
```

## GET `/user/bids` 🔒

Returns a list of active bids for the authenticated user.

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/user/bids \
  --header 'x-archipelago-frontend-token: [YOUR API TOKEN]'
```

### Example Response
{:  .no_toc }

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

## GET `/user/asks` 🔒

Returns a list of active sales for the authenticated user.

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/user/asks \
  --header 'x-archipelago-frontend-token: [YOUR API TOKEN]'
```

### Example Response
{:  .no_toc }

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

## GET `/user/:account/tokens` 🔒

```bash
curl --request GET \
  --url https://api.archipelago.art/v1/user/info \
  --header 'x-archipelago-frontend-token: [YOUR API TOKEN]'
```

### Example Response
{:  .no_toc }

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
