# Task Model

Traditionally Levererat will only handle 1 taskk per delivery, but sometimes  you may wish to add more tasks to a single order.

#### Parameters

| Name                   | Required? | Description                                                  |                       possible values                        |           Default            |
| ---------------------- | :-------: | ------------------------------------------------------------ | :----------------------------------------------------------: | :--------------------------: |
| `start_address`        |    no     | Fully qualified address of where the payload should be picked up at (Parsed via Google Maps Distance matrix API) (Our deliverer will see this field) |                     `string(191)` `null`                     |   `order.creator_address`    |
| `status`               |    no     | Read only field, read more about statuses [here](#here)      | `pending` `assigned` `abandoned` `accepted` `picked_up` `completed` |          `pending`           |
| `end_address`          |    no     | Fully qualified address of where the payload should be delivered at (Parsed via Google Maps Distance matrix API) (Our deliverer will see this field) |                     `string(191)` `null`                     |   `order.contact_address`    |
| `pickup_contact_name`  |    no     | The name of the person/function Levererat couriers can contact before pickup (Our deliverer will see this field) |                     `string(191)` `null`                     |     `order.creator_name`     |
| `pickup_contact_phone` |    no     | E164 Phone number                                            |                     `string(191)` `null`                     |    `order.creator_phone`     |
| `pickup_before_at`     |    no     | When our deliverers can expect the package to be ready for pickup _(This field may be changed by Levererat staff )_ |                     `string(191)` `null`                     |   `order.pickup_ready_at`    |
| `deliver_before_at`    |    no     | When the task should be delivered at _(This field may be changed by Levererat staff )_ |                     `string(191)` `null`                     | `order.must_be_delivered_at` |
| `callback_url`         |    no     | If a valid URL is provided, every time a task changes status, a  `POST`  request will be made, containing [this payload](#taskCallBackUrlPayload) .  Timeout is set to `15 seconds`, and a total of `5 attempts` will be made over a `5 hour period` before the job permanently fails |                    `string(64555)` `null`                    |     `order.callback_url`     |
| `custom_instruction`   |    no     | This will be displayed in red text for our deliverers        |                    `string(64555)` `null`                    |  `order.custom_instruction`  |

#### Example response `POST https://api.levererat.app/partners/v1/orders`

```json
{
    "order": {
        "uuid": "9323894d-7424-4efe-b131-2e12bbea17ab",
        "simple_order_number": "71-12-RFM",
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
        "tasks": [
            {
                "uuid": "9323894d-ff8f-49bb-82fd-61a7173fc476",
                "status": "pending",
                "start_address": "Custom start address, 1",
                "end_address": "Custom end address, 1",
                "pickup_contact_name": "Custom name",
                "pickup_contact_phone": "+461337",
                "callback_url": null,
                "custom_instruction": "Om vi inte är på plats, kolla bakom den gröna ladan",
                "is_end_destination": false
            },
            {
                "uuid": "9323894e-05b3-4e1f-be17-de0460bcebac",
                "status": "pending",
                "start_address": "creator_address_override",
                "end_address": "2936 Sherwood Creek",
                "pickup_contact_name": "creator_name_override",
                "pickup_contact_phone": "+133777",
                "callback_url": "http:\/\/mysite.app\/callback",
                "custom_instruction": null,
                "is_end_destination": false
            }
        ]
    }
}
```

#### <a id="here"></a> Task Status

| Status      | Description                                                 |
| ----------- | ----------------------------------------------------------- |
| `pending`   | Initial task status when created                            |
| `assigned`  | A Levererat coordinator has assigned the task to an courier |
| `abandoned` | The task has been abandoned by the assigned courier         |
| `accepted`  | The task has been accepted by the assigned courier          |
| `picked_up` | The task payload has been picked up by the courier          |
| `completed` | The task has been delivered by the courier                  |

#### <a id="taskCallBackUrlPayload"></a> Task Callback Url Payload

| Field                  | Description                                       | Example value                        |
| ---------------------- | ------------------------------------------------- | ------------------------------------ |
| `order_uuid`           | Order uuid                                        | 9270adbc-ffff-44a5-815e-635ec6b11925 |
| `task_uuid`            | Task uuid                                         | 9270adbd-10ca-4092-aec8-f3daebf4d498 |
| `new_status`           | New task status                                   | completed                            |
| `current_order_status` | State of parent order                             | delivered                            |
| `updated_at`           | When task was updated                             | 2020-05-10 13:37:00                  |
| `task_result`          | If a task is completed, this field will be filled | Misslyckades - ange kommentar        |
| `task_result_comment`  | If a task is completed, this field will be filled | Punka på bilen                       |

