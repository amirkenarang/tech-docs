# MySQL

# Install With Docker

[mysql - Official Image | Docker Hub](https://hub.docker.com/_/mysql)

```bash
docker run --name mysql -e MYSQL_ROOT_PASSWORD=my-secret-pw -d mysql
```

[Connect to MySQL running in Docker container from a local machine | by Md Kamaruzzaman | Towards Data Science](https://towardsdatascience.com/connect-to-mysql-running-in-docker-container-from-a-local-machine-6d996c574e55)

```bash
update mysql.user set host = '%' where user='root';

FLUSH PRIVILEGES;
```