# Prints

## <a id="routes"></a> Routes

| Thing           | Method | URI       |
| --------------- | :----- | :-------- |
| [Print](#index) | `GET`  | `/prints` |

### <a id="index"></a> `GET /prtins?parcel_ids=[id]:...` 

#### Parameters

| Name         | Required? | Description                     |                possible values                 | Default |
| ------------ | :-------: | ------------------------------- | :--------------------------------------------: | :-----: |
| `parcel_ids` |    Yes    | Ids of parcel to include in pdf | `parcels.id` use `:` to fetch multiple parcels |         |



#### Example response `GET https://api.levererat.app/partners/v1/prints?parcel_ids=213:125:523:1254....`

![](https://i.imgur.com/p6LEqvv.png)