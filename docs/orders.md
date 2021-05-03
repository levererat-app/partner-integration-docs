# Orders

## <a id="routes"></a> Routes

| Thing                      | Method | URI                |
| -------------------------- | :----- | :----------------- |
| [List all orders](#index)  | `GET`  | `/orders`          |
| [Get order by UUID](#show) | `GET`  | `/orders/{uuidv4}` |
| [Store new order](#store)  | `POST` | `/orders`          |
| [Update order](#put)       | `PUT`  | `/orders/{uuidv4}` |

### <a id="index"></a> `GET /orders` 

#### Parameters

| Name                 | Required? | Description                   |                       possible values                        |   Default    |
| -------------------- | :-------: | ----------------------------- | :----------------------------------------------------------: | :----------: |
| `status_filter`      |    No     | Filter result based on filter | `all` `pending` `delivered` `accepted_by_company` `declined_by_company` `accepted_by_deliverer` `declined_by_deliverer` |    `all`     |
| `order_by`           |    No     | Sort results based on column  | `created_at` `updated_at` `must_be_delivered_at` `pickup_ready_at` `accepted_by_deliverer_at`  `delivered_at` | `created_at` |
| `order_by_direction` |    No     | Ascend or descend results     |                         `asc` `desc`                         |    `asc`     |

#### Example response `GET https://api.levererat.app/partners/v1/orders`

```json
{
    "orders": {
        "data": [
            {
                "uuid": "932385a9-4cff-4b6f-a031-f4a723aed449",
                "simple_order_number": "67-4-UPP",
                "status": "accepted_by_company",
                "payload": "I eat one of the Queen said to the part about her repeating 'YOU ARE OLD, FATHER WILLIAM,\"' said the Gryphon: and it sat for a moment to think this a good deal frightened at the top with its head.",
                "contact_name": "Karli",
                "contact_phone": "+46701474417",
                "contact_address": "677 Golden Flats Suite 250\nIciemouth, GA 77108",
                "contact_address_postal_code": "15621",
                "creator_name": "Nicole Cronin",
                "creator_phone": "+46701474417",
                "creator_address": "6515 Bettie Cliff Suite 281",
                "must_be_delivered_at": "2021-04-07 18:12:36",
                "pickup_ready_at": "2021-04-07 18:02:36",
                "accepted_by_deliverer_at": null,
                "delivered_at": null,
                "contact_unidentified_at": null,
                "created_at": "2021-04-07 17:02:36",
                "updated_at": "2021-04-07 17:02:36",
                "tasks": []
            }
        ]
    },
    "links": {
        "first": "http:\/\/localhost\/partners\/v1\/orders?page=1",
        "last": "http:\/\/localhost\/partners\/v1\/orders?page=1",
        "prev": null,
        "next": null
    },
    "meta": {
        "current_page": 1,
        "from": 1,
        "last_page": 1,
        "links": [
            {
                "url": null,
                "label": "&laquo; Previous",
                "active": false
            },
            {
                "url": "http:\/\/localhost\/partners\/v1\/orders?page=1",
                "label": "1",
                "active": true
            },
            {
                "url": null,
                "label": "Next &raquo;",
                "active": false
            }
        ],
        "path": "http:\/\/localhost\/partners\/v1\/orders",
        "per_page": 15,
        "to": 1,
        "total": 1
    }
}
```

### <a id="show"></a> `GET /orders/{uuidv4}` 


#### Parameters

_No parameters_

#### Example response `GET https://api.levererat.app/partners/v1/orders/922b...`

```json
{
    "order": {
        "uuid": "932385ad-0494-4d67-9579-284d3c5615b7",
        "simple_order_number": "73-4-ETP",
        "status": "pending",
        "payload": "Oh, how I wish you wouldn't keep appearing and vanishing so suddenly: you make one quite giddy.' 'All right,' said the Cat, 'if you don't explain it as to go nearer till she was small enough to look.",
        "contact_name": "Herminia",
        "contact_phone": "+46701474417",
        "contact_address": "56966 Steuber Divide\nKerluketown, WY 44385",
        "contact_address_postal_code": "31058",
        "creator_name": "Prof. Ramiro Connelly",
        "creator_phone": "+46701474417",
        "creator_address": "208 Stokes Roads Suite 397",
        "must_be_delivered_at": "2021-04-07 18:12:38",
        "pickup_ready_at": "2021-04-07 18:02:38",
        "accepted_by_deliverer_at": null,
        "delivered_at": null,
        "contact_unidentified_at": null,
        "created_at": "2021-04-07 17:02:38",
        "updated_at": "2021-04-07 17:02:38",
        "tasks": []
    }
}
```

### <a id="store"></a> `POST /orders` 

#### Parameters

| Name                          | Required? | Description                                                  |        possible values        |             Default              |
| ----------------------------- | :-------: | ------------------------------------------------------------ | :---------------------------: | :------------------------------: |
| `contact_name`                |    Yes    | Name of end customer                                         |         `string(191)`         |                -                 |
| `contact_address`             |    Yes    | Fully qualified address of end customer (Parsed via Google Maps Distance matrix API) |         `string(191)`         |                -                 |
| `contact_address_postal_code` |    no     | 5 digit postal code, for sorting                             |          `string(5)`          |              `null`              |
| `contact_phone`               |    Yes    | E164 phone number format (+467xxxxx) of end customer         |         `string(191)`         |                -                 |
| `payload`                     |    Yes    | Content of what is going to be delivered, this text is not parsed by levererat.app and will be visible to our couriers |         `mediumText`          |                -                 |
| `pickup_ready_at`             |    Yes    | When our deliverers can expect the package to be ready for pickup |          `dateTime`           |                -                 |
| `must_be_delivered_at`        |    Yes    | When the order should be delivered at                        |          `dateiIme`           |                -                 |
| `test`                        |    no     | Use this to dry-run your order request                       |            `test`             |              `null`              |
| `creator_name`                |    no     | The name of the main customer (Our deliverer will see this field) |     `string(191)` `null`      |  Name of authenticated account   |
| `creator_address`             |    no     | Fully qualified address of the main customer (Parsed via Google Maps Distance matrix API) (Our deliverer will see this field) |     `string(191)` `null`      | Address of authenticated account |
| `creator_phone`               |    no     | E164 phone number format (+467xxxxx) of main customer (Our deliverers will see this field) |     `string(191)` `null`      |  Phone of authenticated account  |
| `tasks`                       |    no     | Add one or more tasks to the given order, if no tasks are given, a default task will be created upon Levererat accepting the order | [Task Model](orders/tasks.md) |               null               |
| `custom_instruction`          |    no     | All child tasks will inherit this field                      |         `mediumText`          |               null               |
| `callback_url`                |    no     | All child tasks will inherit this field                      |         `mediumText`          |               null               |

#### Example response `POST https://api.levererat.app/partners/v1/orders`

```json
{
    "order": {
        "uuid": "932385ab-4d2d-4ec3-97e3-eca0f59fbaa2",
        "simple_order_number": "69-12-WJA",
        "status": "accepted_by_company",
        "payload": "[]",
        "contact_name": "Mrs. Mya Haag II",
        "contact_phone": "+4148750894379",
        "contact_address": "2936 Sherwood Creek",
        "contact_address_postal_code": null,
        "creator_name": "creator_name_override",
        "creator_phone": "+133777",
        "creator_address": "creator_address_override",
        "must_be_delivered_at": "2020-12-04 23:40:38",
        "pickup_ready_at": "2020-12-04 22:40:38",
        "accepted_by_deliverer_at": null,
        "delivered_at": null,
        "contact_unidentified_at": null,
        "created_at": "2020-12-01 23:40:38",
        "updated_at": "2020-12-01 23:40:38",
        "tasks": []
    }
}
```

### <a id="put"></a> `PUT /orders/{uuidv4}` 

#### Parameters

| Name              | Required? | Description                                                  | possible values | Default |
| ----------------- | :-------: | ------------------------------------------------------------ | :-------------: | :-----: |
| `contact_name`    |    No     | Name of end customer                                         |  `string(191)`  |    -    |
| `contact_phone`   |    No     | E164 phone number format (+467xxxxx) of end customer         |  `string(191)`  |    -    |
| `contact_address` |    No     | Fully qualified address of end customer (Parsed via Google Maps Distance matrix API) |  `string(191)`  |    -    |

*Note: Child tasks with* `is_end_destination` *set to* `true` *will have its information changed as well*

#### Example response `PUT https://api.levererat.app/partners/v1/orders/9358...`

```json
{
    "order": {
        "uuid": "93585058-f293-4418-b674-4f57ebe676c4",
        "simple_order_number": "WKL-4-5",
        "status": "pending",
        "payload": "New payload",
        "contact_name": "Mrs. Mya Haag II",
        "contact_phone": "+4148750894379",
        "contact_address": "2936 Sherwood Creek",
        "contact_address_postal_code": "51442",
        "creator_name": "Prof. Cristal Gaylord Sr.",
        "creator_phone": "+46701474417",
        "creator_address": "388 Maximus Stravenue",
        "must_be_delivered_at": "2021-05-04 00:02:24",
        "pickup_ready_at": "2021-05-03 23:52:24",
        "accepted_by_deliverer_at": null,
        "delivered_at": null,
        "contact_unidentified_at": null,
        "created_at": "2021-05-03 22:52:24",
        "updated_at": "2021-05-03 22:52:24",
        "tasks": []
    }
}
```

