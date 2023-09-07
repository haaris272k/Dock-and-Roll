# Docker Practicals

Q: How can I run a container named `blue-app` using the `kodekloud/simple-webapp` image, set the environment variable `APP_COLOR` to "blue," and make the application available on port 38282 on the host?

**A:** Solution:

```bash
docker run -d -p 38282:8080 --name blue-app -e APP_COLOR=blue kodekloud/simple-webapp
```

Q - Deploy a mysql database using the mysql image and name it `mysql-db`.
Set the database password to use `db_pass123`. Lookup the mysql image on Docker Hub and identify the correct environment variable to use for setting the root password.


**A:** Solution:

```bash
docker run --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 -d mysql
```