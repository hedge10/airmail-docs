# Store messages

After a message has been sent successfully, it can be additionally stored. _Airmail_ uses [MongoDB](https://www.mongodb.com/) as storage backend.

To enable message storage set the environment variable `AM_USE_STORAGE` to `true` and configure the connection to the MongoDB database.

| Environment variable    | Default value | Description                           |
| ----------------------- | :------------ | :------------------------------------ |
| `AM_USE_STORAGE`        | `false`       | Store your messages after sending it  |
| `AM_STORAGE_TYPE`       | `mongodb`     | Only `mongodb` is currently supported |
| `AM_MONGODB_HOST`       | `localhost`   | MongoDB host                          |
| `AM_MONGODB_PORT`       | `27017`       | MongoDB port                          |
| `AM_MONGODB_DB`         | `airmail`     | MongoDB database                      |
| `AM_MONGODB_COLLECTION` | `messages`    | MongoDB collection                    |
| `AM_MONGODB_USERNAME`   | _none_        | Username for MongoDB authentication   |
| `AM_MONGODB_PASSWORD`   | _none_        | Password for MongoDB authentication   |

The messages is going to be stored only, if the sending was successful. If an error occured, f. ex. the captcha could not be succesfully verified, neither the sending nor the storage is going to happen.