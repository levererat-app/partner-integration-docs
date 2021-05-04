# Parcels

## <a id="routes"></a> Routes

| Thing                      | Method   | URI                                |
| -------------------------- | :------- | :--------------------------------- |
| [List all parcels](#index) | `GET`    | `/tasks/{taskUuidv4}/parcels`      |
| [Get parcel by id](#show)  | `GET`    | `/tasks/{taskUuidv4}/parcels/{id}` |
| [Store new parcel](#store) | `POST`   | `/tasks/{taskUuidv4}/parcels`      |
| [Delete parcel](#put)      | `DELETE` | `/tasks/{taskUuidv4}/parcels/{id}` |

### <a id="index"></a> `GET /tasks/{taskUuidv4}/parcels` 

#### Parameters

_No parameters_

#### Example response `GET https://api.levererat.app/partners/v1/tasks/935a277e.../parcels`

```json
{
    "parcels": [
        {
            "id": 4,
            "task_uuid": "935a277e-bad8-4a96-8cb1-26f0f296af19",
            "parent_id": null,
            "parent_task_uuid": null,
            "collected_at": null,
            "delivered_at": null,
            "created_at": "2021-05-04 20:49:50"
        }
    ]
}
```

### <a id="show"></a> `GET /tasks/{taskUuidv4}/parcels/{id}` 

#### Parameters

_No parameters_

#### Example response `GET https://api.levererat.app/partners/v1/tasks/935a2781.../parcels/11`

```json
{
    "parcel": {
        "id": 11,
        "task_uuid": "935a2781-b1af-4179-b229-35e410632502",
        "parent_id": null,
        "parent_task_uuid": null,
        "collected_at": null,
        "delivered_at": null,
        "created_at": "2021-05-04 20:49:52"
    }
}
```

### <a id="store"></a> `POST /tasks/{taskUuidv4}/parcels` 

#### Parameters

_No parameters_

_Note:_ Parcels cannot be created if `task.pickup_before_at` is todays date 

#### Example response `POST https://api.levererat.app/partners/v1/tasks/935a277f.../parcels`

```json
{
    "parcel": {
        "id": 6,
        "task_uuid": "935a277f-b31b-4bd7-aa11-d0a79b6a07b4",
        "parent_id": null,
        "parent_task_uuid": null,
        "collected_at": null,
        "delivered_at": null,
        "created_at": "2021-05-04 20:49:50"
    }
}
```

### <a id="store"></a> `DELETE /tasks/{taskUuidv4}/parcels/{id}` 

#### Parameters

_No parameters_

_Note:_ Parcels cannot be deleted if `task.pickup_before_at` is todays date or if `collected_at` or `delivered_at` is not `null`

#### Example response `DELETE https://api.levererat.app/partners/v1/tasks/935a277f.../parcels/16`

```json
{
    "parcel": {
        "id": 16,
        "task_uuid": "935a2784-0d78-4817-a632-423b10ac56fd",
        "parent_id": null,
        "parent_task_uuid": null,
        "collected_at": null,
        "delivered_at": null,
        "created_at": "2021-05-04 20:49:53"
    }
}
```

