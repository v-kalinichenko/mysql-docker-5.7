# MySQL 5.7 Docker
<small>**Latest build:** 2018-02-01</small>

#### Required environmental variables

| Variable | Type | Description |
|----------|------|-------------|
| MYSQL_ROOT_PASSWORD | string | MySQL root user password of either existing database or in case it does not exist it will initialize the new database with the given password. |


### Default mount points

| Docker | Description |
|--------|-------------|
| /var/lib/mysql | MySQL data dir |
| /var/log/mysql | MySQL log dir |
| /var/sock/mysqld | MySQL socket dir 


### Default ports

| Docker | Description |
|--------|-------------|
| 3306   | MySQL listening Port |

## Usage

**1. Listen on loopback interface only**

```bash
$ docker run -i \
    -p 127.0.0.1:3306:3306 \
    -e MYSQL_ROOT_PASSWORD=my-secret-pw \
    -t vkalini/mysql-5.7

# Access MySQL from your host computer
$ mysql --user=root --password=my-secret-pw --host=127.0.0.1 -e 'show databases;'
```

**2. Enable logging**

Enable logging and mount the log directory to your host to `~tmp/mysql-log`
```bash
$ docker run -i \
    -p 127.0.0.1:3306:3306 \
    -v ~tmp/mysql-log:/var/log/mysql \
    -e MYSQL_ROOT_PASSWORD=my-secret-pw \
    -e MYSQL_GENERAL_LOG=1 \
    -t vkalini/mysql-5.7

# Access MySQL from your host computer
$ mysql --user=root --password=my-secret-pw --host=127.0.0.1 -e 'show databases;'
```

**3. Mount MySQL socket to the host**

Use MySQL socket for `localhost` connections through the socket. No need to expose the MySQL port to the host in this case.
```bash
$ docker run -i \
    -v ~tmp/mysql-sock:/var/sock/mysqld \
    -e MYSQL_ROOT_PASSWORD=my-secret-pw \
    -t vkalini/mysql-5.7

# Access MySQL from your host computer via socket
$ mysql --user=root --password=my-secret-pw --socket=/var/sock/mysqld/mysqld.sock -e 'show databases;'
```
