# MongoDB

## USAGE TIPPS
- On POST to a DB via a Connection String `mongodb+srv://myDatabaseUser:D1fficultP%40ssw0rd@cluster0.example.mongodb.net/` the collection allways defaults to test, you have to append a collection name to create a specific collection

## Mongoose

### Models

- Everything in Mongoose starts with a Schema. Each schema maps to a MongoDB collection and defines the shape of the documents within that collection.

- An instance of a model is called a document
- If you want to add additional keys later, use the Schema#add method.