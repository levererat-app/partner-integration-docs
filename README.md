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

The base endpoint for all routes are 

`https://api.levererat.app/partners/v1`

### <a id="rate-limits"></a> Rate limitation

The  limit is 120 requests per  `Access-Token` per minute

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

### <a id="error-codes"></a> HTTP 400 Error codes

All relevant `400 Request Failed` error codes will be listed below

| Code | Meaning                                      |
| ---- | -------------------------------------------- |
| 37   | missing sufficient permissions to view order |

### <a id="authenticate"></a> Authenticate

All requests to the endpoint requires an `Access-Token` provided in your request header or as an request parameter.

The `Access-Token` is bound to your account and is accessible after you sign in for the first time.

### <a id="features"></a> Feature documentation

All features available for the partner integration will be listed below

| Namespace | Base URI  | Docs and examples           |
| --------- | --------- | --------------------------- |
| order     | `/orders` | [Read more](docs/orders.md) |



*Changelog*

* 2021-04-07
  * Removed unused attributes from `Order` `payment_method` `company_swish_ref_id` `company_invoice_ref_id` `company_card_ref_id` . `payment_method` can be replaced with `test`,  
  * New order attribute `test` replacement for `payment_method` and will only be checked for the value "test" for legacy reasons
  * Task status `started` was removed because it was redundant.
  * Added new RO field to tasks `siblings` 
  * Orders have three new fields `contact_address_postal_code` ,  `custom_instruction` and `callback_url`. Tasks will inherit these fields if they are empty.
* 2021-02-10
  * added new TaskModel field `custom_instruction`  [read more here](docs/orders/tasks.md)
* 2021-02-09
  * added two new fields to task http callback `task_result` and `task_result_comment` [read  more here](docs/orders/tasks.md#taskCallBackUrlPayload)
* 2021-02-05
	* added new fields to task http callback `updated_at` 
* 2021-01-09
	* Removed unused column `picked_up_by_deliverer_at` and status types `collected_by_deliverer` 
	* Added new related model `Task` to `order`

