# MongoDB

[Install MongoDB](MongoDB%202337663349b04f34ae625afeea531008/Install%20MongoDB%20717b5ee0470048199f100cfa123700b9.md)

# Dump and Restore

To dump and restore data into the database this article could help you:

[🐳 mongodump and mongorestore with Docker](https://dev.to/mkubdev/mongodump-and-mongorestore-with-docker-39m7)

## Dump

Getting dump and restore it, into a docker is a little different.

To create a dump from the database when the database is into a docker run this command

```bash
docker exec <mongodb container> sh -c 'mongodump --archive' > my-data.dump
```

if it’s not into a docker run this:

```bash
mongodump --host=<IP> --port=<database-port> -u <database-name> -p <password> --archive > my-data.dump

# Example:
mongodump --host=95.217.135.249 --port=27010 -u sensoric -p sensodin1401! --archive > my-data.dump

```

## Restore

To restore data to the database run this command:

```bash
docker exec -i <mongodb container> sh -c 'mongorestore --archive' < my-data.dump
```

## Backup Script

```bash
NOW_IR=$(TZ=":Asia/Tehran" date +'%Y-%m-%d_%H:%M:%S')
ARCHIVE_PATH=/home/
mongodump --host=95.217.135.249 --port=27010 -u uadmin -p 951753 --db sensorik --out $ARCHIVE_PATH/$NOW_IR
cd $ARCHIVE_PATH
zip -r $NOW_IR.zip $NOW_IR
rm -rf ir $NOW_IR
```

# Query and Shell

[Query and Shell](MongoDB%202337663349b04f34ae625afeea531008/Query%20and%20Shell%2049afff8ab59b4384ab600161d0eaef67.md)
