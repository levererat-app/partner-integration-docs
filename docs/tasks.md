# Tasks

## <a id="routes"></a> Routes

| Thing                 | Method | URI                   |
| --------------------- | :----- | :-------------------- |
| [Update a task](#put) | `PUT`  | `/tasks/{taskUuidv4}` |

### <a id="put"></a> `PUT /tasks/{taskUuidv4}` 

#### Parameters

| Name                 | Required? | Description                                                  | possible values | Default |
| -------------------- | :-------: | ------------------------------------------------------------ | :-------------: | :-----: |
| `autocomplete_at_23` |    Yes    | If set to `true` the task will automatically complete itself 23:59 before the day of pickup |    `boolean`    |    -    |

