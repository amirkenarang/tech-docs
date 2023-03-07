# Query and Shell

```bash
db.collection.updateMany(
	{ questionMeta: { $exists: false } },
	{ $set: { "questionMeta": {} } },
  { multi: true }
)
```

```bash
# Change database in mongo compass shell
use <DB-NAME>
# Example:
use sensorik
```

```bash
# Find Exists a filed
{ questionMeta: { $exists: false } }
```

```bash
# Distinct a field
db.answers.distinct( "questionnaireId" )
```

```bash
# like query
{"email": {$regex : "samantest"} }
```

```bash
# for running queries in mongo use the mongo shell. to change the database in mongo use following command:
use <db-name>
```

Other commands:

[MongoDB Shell Commands (tutorialsteacher.com)](https://www.tutorialsteacher.com/mongodb/mongodb-shell-commands#:~:text=mongodb)%5D%20Options%3A%20%2Dh%2C,from%20the%20shell%20during%20the)

```bash
docker exec -it mongodb /bin/bash
bin/mongod --version
```
