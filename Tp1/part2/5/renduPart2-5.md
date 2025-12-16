**Créer un Dockerfile**

 [DockerFile](/Dockerfile)

**Créer un compose.yml**
 [DockerFile](/compose.yml)

**Docker PS :**
docker ps
CONTAINER ID   IMAGE                COMMAND                  CREATED         STATUS         PORTS                                         NAMES
a7f42c44e30e   shitty_app_with_db   "docker-entrypoint.s…"   2 minutes ago   Up 7 seconds   0.0.0.0:3000->3000/tcp, [::]:3000->3000/tcp   5-app-1
67cd6c449563   mysql:8.4            "docker-entrypoint.s…"   2 minutes ago   Up 7 seconds   3306/tcp, 33060/tcp                           5-db-1
97427d11eb96   phpmyadmin           "/docker-entrypoint.…"   7 minutes ago   Up 7 seconds   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp       5-pma-1

**Les log :**
docker compose logs
app-1  | 
pma-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.19.0.3. Set the 'ServerName' directive globally to suppress this message
pma-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.19.0.3. Set the 'ServerName' directive globally to suppress this message
app-1  | > Shitty webapp for B3 Dev TP1@1.0.0 dev
app-1  | > nodemon -L src/app.js
app-1  |
app-1  | [nodemon] 3.1.11
app-1  | [nodemon] to restart at any time, enter `rs`
app-1  | [nodemon] watching path(s): *.*
pma-1  | [Mon Dec 15 15:04:15.333564 2025] [mpm_prefork:notice] [pid 1:tid 1] AH00163: Apache/2.4.65 (Debian) PHP/8.3.28 configured -- resuming normal operations
pma-1  | [Mon Dec 15 15:04:15.333829 2025] [core:notice] [pid 1:tid 1] AH00094: Command line: 'apache2 -D FOREGROUND'
pma-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.19.0.3. Set the 'ServerName' directive globally to suppress this message
pma-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.19.0.3. Set the 'ServerName' directive globally to suppress this message
pma-1  | [Mon Dec 15 15:05:34.583724 2025] [mpm_prefork:notice] [pid 1:tid 1] AH00163: Apache/2.4.65 (Debian) PHP/8.3.28 configured -- resuming normal operations
pma-1  | [Mon Dec 15 15:05:34.584249 2025] [core:notice] [pid 1:tid 1] AH00094: Command line: 'apache2 -D FOREGROUND'
pma-1  | [Mon Dec 15 15:07:12.293018 2025] [mpm_prefork:notice] [pid 1:tid 1] AH00170: caught SIGWINCH, shutting down gracefully        
pma-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.19.0.3. Set the 'ServerName' directive globally to suppress this message
pma-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.19.0.3. Set the 'ServerName' directive globally to suppress this message
pma-1  | [Mon Dec 15 15:07:17.613577 2025] [mpm_prefork:notice] [pid 1:tid 1] AH00163: Apache/2.4.65 (Debian) PHP/8.3.28 configured -- resuming normal operations
app-1  | [nodemon] watching extensions: js,mjs,cjs,json
app-1  | [nodemon] starting `node src/app.js`
app-1  | Waiting for database... (1/30)
app-1  | Database ready
app-1  | Server running on port 3000
app-1  |
app-1  | > Shitty webapp for B3 Dev TP1@1.0.0 dev
db-1   | 2025-12-15 15:09:03+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.4.7-1.el9 started.
db-1   | 2025-12-15 15:09:04+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
db-1   | 2025-12-15 15:09:04+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.4.7-1.el9 started.
db-1   | '/var/lib/mysql/mysql.sock' -> '/var/run/mysqld/mysqld.sock'
db-1   | 2025-12-15T15:09:04.652021Z 0 [System] [MY-015015] [Server] MySQL Server - start.
db-1   | 2025-12-15T15:09:04.913977Z 0 [System] [MY-010116] [Server] /usr/sbin/mysqld (mysqld 8.4.7) starting as process 1
db-1   | 2025-12-15T15:09:04.921594Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
db-1   | 2025-12-15T15:09:05.411525Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
db-1   | 2025-12-15T15:09:05.626705Z 0 [System] [MY-010229] [Server] Starting XA crash recovery...
db-1   | 2025-12-15T15:09:05.639452Z 0 [System] [MY-010232] [Server] XA crash recovery finished.
db-1   | 2025-12-15T15:09:05.726066Z 0 [Warning] [MY-010068] [Server] CA certificate ca.pem is self signed.
db-1   | 2025-12-15T15:09:05.726132Z 0 [System] [MY-013602] [Server] Channel mysql_main configured to support TLS. Encrypted connections are now supported for this channel.
db-1   | 2025-12-15T15:09:05.729469Z 0 [Warning] [MY-011810] [Server] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
db-1   | 2025-12-15T15:09:05.778862Z 0 [System] [MY-011323] [Server] X Plugin ready for connections. Bind-address: '::' port: 33060, socket: /var/run/mysqld/mysqlx.sock
db-1   | 2025-12-15T15:09:05.779129Z 0 [System] [MY-010931] [Server] /usr/sbin/mysqld: ready for connections. Version: '8.4.7'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server - GPL.
db-1   | 2025-12-15T15:11:19.808889Z 0 [System] [MY-013172] [Server] Received SHUTDOWN from user <via user signal>. Shutting down mysqld (Version: 8.4.7).
db-1   | 2025-12-15 15:11:25+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.4.7-1.el9 started.
db-1   | 2025-12-15 15:11:26+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
db-1   | 2025-12-15 15:11:26+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.4.7-1.el9 started.
db-1   | '/var/lib/mysql/mysql.sock' -> '/var/run/mysqld/mysqld.sock'
db-1   | 2025-12-15T15:11:26.616712Z 0 [System] [MY-015015] [Server] MySQL Server - start.
db-1   | 2025-12-15T15:11:26.872375Z 0 [System] [MY-010116] [Server] /usr/sbin/mysqld (mysqld 8.4.7) starting as process 1
db-1   | 2025-12-15T15:11:26.890610Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
db-1   | 2025-12-15T15:11:27.407478Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
db-1   | 2025-12-15T15:11:27.630758Z 0 [System] [MY-010229] [Server] Starting XA crash recovery...
db-1   | 2025-12-15T15:11:27.642854Z 0 [System] [MY-010232] [Server] XA crash recovery finished.
db-1   | 2025-12-15T15:11:27.727294Z 0 [Warning] [MY-010068] [Server] CA certificate ca.pem is self signed.
db-1   | 2025-12-15T15:11:27.727349Z 0 [System] [MY-013602] [Server] Channel mysql_main configured to support TLS. Encrypted connections are now supported for this channel.
db-1   | 2025-12-15T15:11:27.731069Z 0 [Warning] [MY-011810] [Server] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
db-1   | 2025-12-15T15:11:27.782125Z 0 [System] [MY-011323] [Server] X Plugin ready for connections. Bind-address: '::' port: 33060, socket: /var/run/mysqld/mysqlx.sock
pma-1  | [Mon Dec 15 15:07:17.624872 2025] [core:notice] [pid 1:tid 1] AH00094: Command line: 'apache2 -D FOREGROUND'
pma-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.19.0.3. Set the 'ServerName' directive globally to suppress this message
pma-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.19.0.3. Set the 'ServerName' directive globally to suppress this message
pma-1  | [Mon Dec 15 15:09:04.103159 2025] [mpm_prefork:notice] [pid 1:tid 1] AH00163: Apache/2.4.65 (Debian) PHP/8.3.28 configured -- resuming normal operations
pma-1  | [Mon Dec 15 15:09:04.103280 2025] [core:notice] [pid 1:tid 1] AH00094: Command line: 'apache2 -D FOREGROUND'
pma-1  | [Mon Dec 15 15:11:19.835575 2025] [mpm_prefork:notice] [pid 1:tid 1] AH00170: caught SIGWINCH, shutting down gracefully        
app-1  | > nodemon -L src/app.js
app-1  |
app-1  | [nodemon] 3.1.11
app-1  | [nodemon] to restart at any time, enter `rs`
app-1  | [nodemon] watching path(s): *.*
app-1  | [nodemon] watching extensions: js,mjs,cjs,json
app-1  | [nodemon] starting `node src/app.js`
app-1  | Waiting for database... (1/30)
app-1  | Database ready
db-1   | 2025-12-15T15:11:27.783835Z 0 [System] [MY-010931] [Server] /usr/sbin/mysqld: ready for connections. Version: '8.4.7'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server - GPL.
pma-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.19.0.3. Set the 'ServerName' directive globally to suppress this message
pma-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.19.0.3. Set the 'ServerName' directive globally to suppress this message
pma-1  | [Mon Dec 15 15:11:26.037443 2025] [mpm_prefork:notice] [pid 1:tid 1] AH00163: Apache/2.4.65 (Debian) PHP/8.3.28 configured -- resuming normal operations
pma-1  | [Mon Dec 15 15:11:26.037827 2025] [core:notice] [pid 1:tid 1] AH00094: Command line: 'apache2 -D FOREGROUND'
app-1  | Server running on port 3000
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\5> 

**Curl**
``` bash
curl http://localhost:3000

    <h1>Simple DB App</h1>
      <img src="https://http.cat/images/200.jpg" alt="HTTP Cat 200 - OK">
    <h2>Add User</h2>
    <form method="POST" action="/add">
      <input type="text" name="pseudo" placeholder="Enter pseudo" required>
      <button>Add</button>
```

``` bash
curl http://localhost:8080
<!doctype html>
<html lang="en" dir="ltr">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="referrer" content="same-origin">
  <meta name="robots" content="noindex,nofollow,notranslate">
  <meta name="google" content="notranslate">
  <style id="cfs-style">html{display: none;}</style>
  <link rel="icon" href="favicon.ico" type="image/x-icon">
  <link rel="shortcut icon" href="favicon.ico" type="image/x-icon">
  <link rel="stylesheet" type="text/css" href="./themes/pmahomme/jquery/jquery-ui.css">
  <link rel="stylesheet" type="text/css" href="js/vendor/codemirror/lib/codemirror.css?v=5.2.3">
  <link rel="stylesheet" type="text/css" href="js/vendor/codemirror/addon/hint/show-hint.css?v=5.2.3">
  <link rel="stylesheet" type="text/css" href="js/vendor/codemirror/addon/lint/lint.css?v=5.2.3">
  <link rel="stylesheet" type="text/css" href="./themes/pmahomme/css/theme.css?v=5.2.3">
  <title>phpMyAdmin</title>
 
```