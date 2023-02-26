# connection with mongoDatabase 

/alert  if mongo_uri not work write **127.0.0.1** instead of **localhost**

## first download dependencies
```
npm i mongodb
```

## second create db.ts file and write the following code
```
import { MongoClient } from 'mongodb';
import { MONGODB_URI, DATABASE_NAME } from './config';

let connectedClient;

export const connectClient = async () => {
  /// to use cached client
  if (connectedClient) {
    return connectedClient.db(DATABASE_NAME);
  }
  const client = new MongoClient(MONGODB_URI);
  await client.connect();
  await client.db(DATABASE_NAME).command({ ping: 1 });
  console.info('database connected successfully');

  connectedClient = client;

  return connectedClient.db(DATABASE_NAME);
};

export const stopClient = async () => {
  return connectedClient?.close();
};

```