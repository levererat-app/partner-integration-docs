# Orders

## <a id="routes"></a> Routes

| method | uri                |
| :----- | :----------------- |
| `GET`  | `/orders`          |
| `GET`  | `/orders/{uuidv4}` |
| `POST` | `/orders`          |

### <a id="index"></a> `GET /orders` 

#### Parameters

| Name               | Required? | Description                   |                       possible values                        |   Default    |
| ------------------ | :-------: | ----------------------------- | :----------------------------------------------------------: | :----------: |
| `statusFilter`     |    No     | Filter result based on filter | `all ` `pending` `delivered` `declined_by_payment` `accepted_by_company` `declined_by_company` `accepted_by_deliverer` `declined_by_deliverer` ` collected_by_deliverer` `picked_up_by_deliverer` |    `all`     |
| `orderBy`          |    No     | Sort results based on column  | ` created_at`  ` updated_at` ` must_be_delivered_at` ` pickup_ready_at`  ` accepted_by_deliverer_at` ` picked_up_by_deliverer_at` ` delivered_at` | `created_at` |
| `orderByDirection` |    No     | Ascend or descend results     |                         `asc` `desc`                         |    `asc`     |



#### Example response `https://api.levererat.app/partners/v1/orders`

```json
{
    "orders": {
        "data": [
            {
                "uuid": "922bc46d-41f0-451b-a6c4-95e83b461456",
                "simple_order_number": "83-12-2",
                "status": "accepted_by_company",
                "payment_method": "levererat_swish",
                "company_swish_ref_id": null,
                "company_invoice_ref_id": null,
                "company_card_ref_id": null,
                "payload": "Ugh, Serpent!' 'But I'm not myself, you see.' 'I don't think they play at all what had become of me?' Luckily for Alice, the little door: but, alas! the little door about fifteen inches high: she.",
                "contact_name": "Dashawn",
                "contact_phone": "+46701474417",
                "contact_address": "96950 Blanda Square\nEast Marielleville, OH 53983-1813",
                "creator_name": "Ryder Rosenbaum",
                "creator_phone": "+46701474417",
                "creator_address": "127 Rogahn Light Suite 306",
                "must_be_delivered_at": "2020-12-05 13:22:47",
                "pickup_ready_at": "2020-12-05 13:12:47",
                "accepted_by_deliverer_at": null,
                "picked_up_by_deliverer_at": null,
                "delivered_at": null,
                "contact_unidentified_at": null,
                "created_at": "2020-12-05 12:12:47",
                "updated_at": "2020-12-05 12:12:48"
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
                "label": 1,
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

#### Example response `https://api.levererat.app/partners/v1/orders/922b...`

```json
{
    "order": {
        "uuid": "922bc46f-aef1-4ab0-b5a6-e97b3fcfe824",
        "simple_order_number": "88-12-2",
        "status": "pending",
        "payment_method": "levererat_swish",
        "company_swish_ref_id": null,
        "company_invoice_ref_id": null,
        "company_card_ref_id": null,
        "payload": "All on a little different. But if I'm not the smallest notice of her voice, and see how he can thoroughly enjoy The pepper when he sneezes; For he can thoroughly enjoy The pepper when he sneezes.",
        "contact_name": "Lance",
        "contact_phone": "+46701474417",
        "contact_address": "2188 Rashad Squares\nPort Emmanuelshire, OH 48458-8288",
        "creator_name": "Hortense Hodkiewicz",
        "creator_phone": "+46701474417",
        "creator_address": "622 Zulauf Harbor",
        "must_be_delivered_at": "2020-12-05 13:22:49",
        "pickup_ready_at": "2020-12-05 13:12:49",
        "accepted_by_deliverer_at": null,
        "picked_up_by_deliverer_at": null,
        "delivered_at": null,
        "contact_unidentified_at": null,
        "created_at": "2020-12-05 12:12:49",
        "updated_at": "2020-12-05 12:12:49"
    }
}
```

### <a id="show"></a> `POST /orders` 

#### Parameters

| Name                     |                Required?                 | Description                                                  |                       possible values                        |             Default              |
| ------------------------ | :--------------------------------------: | ------------------------------------------------------------ | :----------------------------------------------------------: | :------------------------------: |
| `contact_name`           |                   Yes                    | Name of end customer                                         |                        `string(191)`                         |                -                 |
| `contact_address`        |                   Yes                    | Fully qualified address of end customer (Parsed via Google Maps Distance matrix API) |                        `string(191)`                         |                -                 |
| `contact_phone`          |                   Yes                    | E164 phone number format (+467xxxxx) of end customer         |                        `string(191)`                         |                -                 |
| `payload`                |                   yes                    | Content of what is going to be delivered, this text is not parsed by levererat.app and will be visible to our deliverers |                         `mediumText`                         |                -                 |
| `pickup_ready_at`        |                   yes                    | When our deliverers can expect the package to be ready for pickup |                          `dateTime`                          |                -                 |
| `must_be_delivered_at`   |                   yes                    | When the order should be delivered at                        |                          `dateiIme`                          |                -                 |
| `payment_method`         |                   yes                    | What kind of payment method that should be used, payments methods starting with `levererat` is our own payment solutions. If you already have a payment solution in place, you could use any of the `company_` payment methods | `levererat_swish` `company_swish` `company_invoice` `company_card` |                -                 |
| `company_swish_ref_id`   |  if `payment_method` is `company_swish`  | This field is used to keep track of orders                   |                        `string(191)`                         |                                  |
| `company_invoice_ref_id` | if `payment_method` is `company_invoice` | This field is used to keep track of orders                   |                        `string(191)`                         |              `null`              |
| `company_card_ref_id`    |  If `payment_method` is `company_card`   | This field is used to keep track of orders                   |                        `string(191)`                         |              `null`              |
| `creator_name`           |                    no                    | The name of the main customer (Our deliverer will see this field) |                     `string(191)` `null`                     |  Name of authenticated account   |
| `creator_address`        |                    no                    | Fully qualified address of the main customer (Parsed via Google Maps Distance matrix API) (Our deliverer will see this field) |                     `string(191)` `null`                     | Address of authenticated account |
| `creator_phone`          |                    no                    | E164 phone number format (+467xxxxx) of main customer (Our deliverers will see this field) |                     `string(191)` `null`                     |  Phone of authenticated account  |

#### Example response `https://api.levererat.app/partners/v1/orders`

```json
{
    "order": {
        "uuid": "922bc46f-1571-4be9-85f9-039360e0b6c6",
        "simple_order_number": "86-12-2",
        "status": "accepted_by_company",
        "payment_method": "company_invoice",
        "company_swish_ref_id": null,
        "company_invoice_ref_id": 'Fortnox-invoice-29192',
        "company_card_ref_id": null,
        "payload": "[]",
        "contact_name": "Mrs. Mya Haag II",
        "contact_phone": "+4148750894379",
        "contact_address": "2936 Sherwood Creek",
        "creator_name": "creator_name_override",
        "creator_phone": "+133777",
        "creator_address": "creator_address_override",
        "must_be_delivered_at": "2020-12-04 22:40:38",
        "pickup_ready_at": "2020-12-04 22:40:38",
        "accepted_by_deliverer_at": null,
        "picked_up_by_deliverer_at": null,
        "delivered_at": null,
        "contact_unidentified_at": null,
        "created_at": "2020-12-05 12:12:48",
        "updated_at": "2020-12-05 12:12:48"
    }
}
```
