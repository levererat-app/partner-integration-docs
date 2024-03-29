<p align="center"><img src="https://levererat.app/logo_transparent.png" style="max-width:300px"></p>

# About Levererat.app partner integration

We provide a RESTful API for our partners.

## Table of contents
* [Endpoint](#endpoint)
* [Rate limitation](#rate-limits)
* [Status codes](#status-codes)
* [HTTP 400 Error codes](#error-codes)
* [Authenticate](#authenticate)
* [Feature documentation](#features)

### <a id="endpoint"></a> Endpoint

*For production*

`https://api.levererat.app/partners/v1`

*For stage/dev*

`https://stage.api.levererat.app/partners/v1`

### <a id="rate-limits"></a> Rate limitation

The  limit is 600 requests per  `Access-Token` per minute

### <a id="status-code"></a> Status codes

Our API can return 8 different status codes

| Status code | Meaning                               | Returns |
| :---------: | ------------------------------------- | ------- |
|     200     | Successfully retrieved resource       | JSON    |
|     201     | Successfully created resource         | JSON    |
|     400     | Request failed, more info in response | JSON    |
|     403     | Forbidden because of permissions      | -       |
|     404     | Resource not found                    | -       |
|     422     | Request failed, more info in response | JSON    |
|     429     | To many requests                      | -       |
|     500     | Server error                          | -       |

### <a id="authenticate"></a> Authenticate

All requests to the endpoint requires an `Access-Token` provided in your request header or as an request parameter.

The `Access-Token` is bound to your account and is accessible after you sign in for the first time.

### <a id="features"></a> Feature documentation

All features available for the partner integration will be listed below

| Namespace     | Base URI                      | Docs and examples            | Related Models                     |
| ------------- | ----------------------------- | ---------------------------- | ---------------------------------- |
| order         | `/orders`                     | [Read more](docs/orders.md)  | [Task Model](docs/orders/tasks.md) |
| tasks         | `/tasks`                      | [Read more](docs/tasks.md)   |                                    |
| tasks.parcels | `/tasks/{taskUuidv4}/parcels` | [Read more](docs/parcels.md) |                                    |
| prints        | `/prints`                     | [Read more](docs/prints.md)  |                                    |

