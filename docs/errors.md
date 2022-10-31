---
layout: default
title: Errors
nav_order: 3
---

# 🚫 Errors

Archipelago uses the conventional HTTP response codes to indicate the success or failure of an API request. The table below lists the most common error codes and their meanings.

## Status Codes

| Status Code            | Summary                                                                                  |
| :--------------------- | :--------------------------------------------------------------------------------------- |
| **200** - OK           | Everything worked as expected.                                                           |
| **400** - Bad Request  | The request was not structured properly, often due to a missing parameter. |
| **401** - Unauthorized | No valid API key was provided, or the API key is invalid.                                |
| **404** - Not Found    | The requested API resource was not found.                                                |
| **500** - Server Error | Something went wrong on the Archipelago end. Please retry the request.                   |

# 🐎 Rate Limits

The Archipelago API enforces rate limits for each client. Every response from the Archipelago API includes two headers related to rate limits:

- `x-rate-limit-max`: the maximum request limit for your token, by default this is `40`
- `x-rate-limit-remaining`: the capacity remaining out of the total limit

The `x-rate-limit-remaining` header will change based on the number of requests made.

**Importantly**, if the rate limit is reached, a 429 HTTP error code will be returned from the API.
