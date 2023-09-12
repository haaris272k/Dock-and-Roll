# Docker Practicals
#### *Note - Just focus on to crafting the commands*

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


Q - create a simple container called `clickcounter` with the image `kodekloud/click-counter`, link it to the `redis` container (create a redis container first) and then expose it on the  `host port 8085`. The clickcounter app run on port `5000`.

**A:** Solution:

```bash

docker run --name=redis redis

docker run -d --name=clickcounter --link redis:redis -p 8085:5000 kodekloud/click-counter
```
