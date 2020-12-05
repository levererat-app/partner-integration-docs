# Orders

## <a id="routes"></a> Routes

| method | namespace | uri              | docs                              |
| ------ | --------- | ---------------- | --------------------------------- |
| `GET`  | order     | `/orders`        | [Read more](#index) |
| `POST` | order     | `/orders`        | [Read more](#store) |
| `GET`  | order     | `/orders/{uuid}` | [Read more](#show)  |

### <a id="index"></a> `GET /orders` 

#### Parameters

| Name               | Required? | Description                   |                       possible values                        |   Default    |
| ------------------ | :-------: | ----------------------------- | :----------------------------------------------------------: | :----------: |
| `statusFilter`     |    No     | Filter result based on filter | `all ` `pending` `delivered` `declined_by_payment` `accepted_by_company` `declined_by_company` `accepted_by_deliverer` `declined_by_deliverer` ` collected_by_deliverer` `picked_up_by_deliverer` |    `all`     |
| `orderBy`          |    No     | Sort results based on column  | ` created_at`  ` updated_at` ` must_be_delivered_at` ` pickup_ready_at`  ` accepted_by_deliverer_at` ` picked_up_by_deliverer_at` ` delivered_at` | `created_at` |
| `orderByDirection` |    No     | Ascend or descend results     |                         `asc` `desc`                         |    `asc`     |

##### Example response

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