# Task Model

Traditionally Levererat will only handle 1 order per delivery, but sometimes  you may wish to add more tasks to a single order.

#### Parameters

| Name                   | Required? | Description                                                  |                       possible values                        |           Default            |
| ---------------------- | :-------: | ------------------------------------------------------------ | :----------------------------------------------------------: | :--------------------------: |
| `start_address`        |    no     | Fully qualified address of where the payload should be picked up at (Parsed via Google Maps Distance matrix API) (Our deliverer will see this field) |                     `string(191)` `null`                     |   `order.creator_address`    |
| `status`               |    no     | Read only field, read more about statuses [here](#here)      | `pending` `assigned` `abandoned` `accepted` `started` `picked_up` `completed` |          `pending`           |
| `end_address`          |    no     | Fully qualified address of where the payload should be delivered at (Parsed via Google Maps Distance matrix API) (Our deliverer will see this field) |                     `string(191)` `null`                     |   `order.contact_address`    |
| `pickup_contact_name`  |    no     | The name of the person/function Levererat couriers can contact before pickup (Our deliverer will see this field) |                     `string(191)` `null`                     |     `order.creator_name`     |
| `pickup_contact_phone` |    no     | E164 Phone number                                            |                     `string(191)` `null`                     |    `order.creator_phone`     |
| `pickup_before_at`     |    no     | When our deliverers can expect the package to be ready for pickup _(This field may be changed by Levererat staff )_ |                     `string(191)` `null`                     |   `order.pickup_ready_at`    |
| `deliver_before_at`    |    no     | When the task should be delivered at _(This field may be changed by Levererat staff )_ |                     `string(191)` `null`                     | `order.must_be_delivered_at` |
| `callback_url`         |    no     | If a valid URL is provided, every time a task changes status, a  ` POST`  request will be made, containing this payload `{"order_uuid": "44f3...", "task_uuid": "44f3...", "new_status": "picked_up"}` .  Timeout is set to `15 seconds`, and a total of `5 attempts` will be made over a `5 hour period` before the job permanently fails |                    `string(64555)` `null`                    |            `null`            |

#### Example response `POST https://api.levererat.app/partners/v1/orders`

```json
{
    "order": {
        "uuid": "9270adbc-ffff-44a5-815e-635ec6b11925",
        "simple_order_number": "63-12-1",
        "status": "accepted_by_company",
        "payment_method": "company_invoice",
        "company_swish_ref_id": null,
        "company_invoice_ref_id": null,
        "company_card_ref_id": null,
        "payload": "[]",
        "contact_name": "Mrs. Mya Haag II",
        "contact_phone": "+4148750894379",
        "contact_address": "2936 Sherwood Creek",
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
        "tasks": [
            {
                "uuid": "9270adbd-10ca-4092-aec8-f3daebf4d498",
                "status": "pending",
                "start_address": "Custom start address, 1",
                "end_address": "Custom end address, 1",
                "pickup_contact_name": "Custom name",
                "pickup_contact_phone": "+461337",
                "callback_url": null
            },
            {
                "uuid": "9270adbd-16f1-41f8-aa03-78f85a50cba2",
                "status": "pending",
                "start_address": "creator_address_override",
                "end_address": "2936 Sherwood Creek",
                "pickup_contact_name": "creator_name_override",
                "pickup_contact_phone": "+133777",
                "callback_url": "http:\/\/mysite.app\/callback"
            }
        ]
    }
}
```

#### <a id="here"></a Task Status

| Status      | Description                                                 |
| ----------- | ----------------------------------------------------------- |
| `pending`   | Initial task status when created                            |
| `assigned`  | A Levererat coordinator has assigned the task to an courier |
| `abandoned` | The task has been abandoned by the assigned courier         |
| `accepted`  | The task has been accepted by the assigned courier          |
| `picked_up` | The task payload has been picked up by the courier          |
| `completed` | The task has been delivered by the courier                  |

