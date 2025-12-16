# DokerRendu

---

**Lancez un conteneur mysql en version 8.4:**

```bash
 docker run --name mysql mysql:8.4
```

---

**Vérifier que le conteneur est actif**

```bash
docker ps -a

CONTAINER ID   IMAGE       COMMAND                  CREATED         STATUS                     PORTS     NAMES
3e840b6e1204   mysql:8.4   "docker-entrypoint.s…"   4 minutes ago   Exited (1) 4 minutes ago             mysql
```

---

**Consulter les logs du conteneur**

```bash
docker logs 3e840b6e1204

2025-12-15 09:53:01+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.4.7-1.el9 started.
2025-12-15 09:53:01+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
2025-12-15 09:53:01+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.4.7-1.el9 started.
2025-12-15 09:53:01+00:00 [ERROR] [Entrypoint]: Database is uninitialized and password option is not specified
    You need to specify one of the following as an environment variable:
    - MYSQL_ROOT_PASSWORD
    - MYSQL_ALLOW_EMPTY_PASSWORD
    - MYSQL_RANDOM_ROOT_PASSWORD
```

---

**Supprimer le conteneur inactif**

```bash
PS C:\Users\russi> docker rm 3e840b6e1204
3e840b6e1204
PS C:\Users\russi> docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
PS C:\Users\russi>
```

---

**Lancer un nouveau conteneur MySQL**

```bash
docker run --name mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:8.4
079161eb48121961b9397fb4d4a312c695b7cc253eba61c1a0ee662a9bf8be94
```

---

**Lancer un conteneur PHPMyAdmin**

```bash
docker run --name phpmyadmin -d --link mysql:db -p 8080:80 phpmyadmin
ea4f44eeeb19fee96d9cf64dcb3ba2e1341c5c970e991e5dd5d8cf71bcc34ccd
```

---

**Visitez l'interface web de PHPMyAdmin**

```bash
curl http://localhost:8080
<!doctype html>
<html lang="en" dir="ltr">
<head>
  <meta charset="utf-8">
```

---

**Remplacer par les bonnes valeurs**

```bash
services:
  db:
    image: mysql:8.4
    environment:
      - MYSQL_ROOT_PASSWORD=root

  pma:
    image: phpmyadmin
    ports:
      - "8080:80"
```

---

**Lancer la stack compose**

```bash
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu> docker compose up
[+] Running 1/1
 ✔ Container dokerrendu-db-1  Running                                                                                                                                                    0.0s
Attaching to db-1, pma-1
pma-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.18.0.2. Set the 'ServerName' directive globally to suppress this message
pma-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.18.0.2. Set the 'ServerName' directive globally to suppress this message
```

---

**Visitez l'interface Web de PHPMyAdmin**

```bash
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu> curl http://localhost:8080
<!doctype html>
<html lang="en" dir="ltr">
<head>
```

---

**Ajouter la gestion d'un volume à votre compose.yml**

```yaml
services:
  db:
    image: mysql:8.4
    environment:
      - MYSQL_ROOT_PASSWORD=root
    volumes:
      - db_data:/var/lib/mysql

  pma:
    image: phpmyadmin
    ports:
      - "8080:80"

volumes:
  db_data:
```

---

**Prouver que le volume est bien utilisé**

```bash
docker volume ls
DRIVER    VOLUME NAME
local     1a3fe18f983a77eda4d847c8821584069271f259e4cf8d04e872c0a7e12aa3b2
local     6e22443d39bb3acd0100efc4441018059ae7661cd05abe02d75f62d462c8364d
local     97b9032aaa7d089e549b0f7273c87f7a751e77da6e1164ba54fb61de0802d82b
local     a855843158277e0daad7c522dc8e3235273ecfd38f49dc3867e18a013f7f704e
local     dokerrendu_db_data
local     express-archi-test-qualite_postgres_data
local     express-archi-test-qualite_sonardb_data
local     express-archi-test-qualite_sonarqube_data
local     express-archi-test-qualite_sonarqube_extensions
local     express-archi-test-qualite_sonarqube_logs
local     f02d0ade1aad78027452f3df515cd64cdf407caba4bab2c134df46c376a4b15d
local     f671457c054f80c08c89ca371cb9749867c1b220f1c9ae8a7ad3c6c2d028f2cd
```

---

**Proposer un nouveau compose.yml**

[Fichier compose modifier](compose.yml)

---

# 2. Dockerfile

**Récupérez le package.json et app.js que je vous ai cook**

[package](/part2/1/package.json)
[app](/part2/1/src/app.js)

---

**Ajoutez un fichier part2/1/Dockerfile**

[Dockerfile](Dockerfile)

---

**Construire l'image shitty_app à partir de ce Dockerfile**

```
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1> docker run -p 3000:3000 -d shitty_app:1.0        
b6e910c0a50f99d1fdcdbedf5faae63e8cfa4acf5fd5643ae25c8b15aea4d4db
```

---

**Prouvez que ça tourne**

```bash
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1> docker ps
CONTAINER ID   IMAGE            COMMAND                  CREATED          STATUS          PORTS                                         NAMES
b6e910c0a50f   shitty_app:1.0   "docker-entrypoint.s…"   53 seconds ago   Up 52 seconds   0.0.0.0:3000->3000/tcp, [::]:3000->3000/tcp   focused_proskuriakova

PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1> docker logs b6

> Shitty webapp for B3 Dev TP1@1.0.0 dev
> nodemon -L src/app.js

[nodemon] 3.1.11
[nodemon] to restart at any time, enter `rs`
[nodemon] watching path(s): *.*
[nodemon] watching extensions: js,mjs,cjs,json
[nodemon] starting `node src/app.js`
Server running at http://localhost:3000

PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1> curl http://localhost:3000

    <!DOCTYPE html>
    <html>
      <head>
        <title>HTTP Cat</title>
```

---

# 3 Hot reload

**Lancer un nouveau conteneur à partir de l'image shitty_app**

```bash
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1> docker ps     
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1> docker run -p 3000:3000 -d -v "C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1\src:/app/src" shitty_app:1.0
bfc4b1a80a0a976a21c9685c1d52322b17545f9442f541daf630c6c3bb817a27
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1> docker ps                                                             
CONTAINER ID   IMAGE            COMMAND                  CREATED         STATUS         PORTS                                         NAMES
bfc4b1a80a0a   shitty_app:1.0   "docker-entrypoint.s…"   5 seconds ago   Up 4 seconds   0.0.0.0:3000->3000/tcp, [::]:3000->3000/tcp   stupefied_euclid
```

---

**Vérifier que ça fonctionne**

```bash
docker logs b6
> Shitty webapp for B3 Dev TP1@1.0.0 dev
> nodemon -L src/app.js

[nodemon] 3.1.11
[nodemon] to restart at any time, enter `rs`
[nodemon] watching path(s): *.*
[nodemon] watching extensions: js,mjs,cjs,json
[nodemon] starting `node src/app.js`
Server running at http://localhost:3000
```

---

# 4. Compose

**Transformer ce docker run en compose.yml**

```yaml
services:
  app:
    image: shitty_app:1.0
    ports:
      - "3000:3000"
    volumes:
      - ./src:/app/src
      - ./package.json:/app/package.json
```

```bash
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1> docker compose up
Attaching to app-1
Gracefully Stopping... press Ctrl+C again to force
Error response from daemon: failed to set up container networking: driver failed programming external connectivity on endpoint 1-app-1 (633f65f8438c1f82066cd71bda8f7ae1ab580d574b413ac9e692835345194690): Bind for 0.0.0.0:3000 failed: port is already allocated
```

---

# 5. DB

**Créer un Dockerfile**

 [DockerFile](/Dockerfile)

---

**Créer un compose.yml**

 [DockerFile](/compose.yml)

---

**Docker PS :**

```
docker ps
CONTAINER ID   IMAGE                COMMAND                  CREATED         STATUS         PORTS                                         NAMES
a7f42c44e30e   shitty_app_with_db   "docker-entrypoint.s…"   2 minutes ago   Up 7 seconds   0.0.0.0:3000->3000/tcp, [::]:3000->3000/tcp   5-app-1
67cd6c449563   mysql:8.4            "docker-entrypoint.s…"   2 minutes ago   Up 7 seconds   3306/tcp, 33060/tcp                           5-db-1
97427d11eb96   phpmyadmin           "/docker-entrypoint.…"   7 minutes ago   Up 7 seconds   0.0.0.0:8080->80/tcp, [::]:8080->80/tcp       5-pma-1
```

---

**Les log :**

```
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
...
```

---

**Curl**

```bash
curl http://localhost:3000

    <h1>Simple DB App</h1>
      <img src="https://http.cat/images/200.jpg" alt="HTTP Cat 200 - OK">
    <h2>Add User</h2>
    <form method="POST" action="/add">
      <input type="text" name="pseudo" placeholder="Enter pseudo" required>
      <button>Add</button>
```

```bash
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

