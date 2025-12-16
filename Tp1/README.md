# DokerRendu

**Lancez un conteneur mysql en version 8.4:**

```bash
 docker run --name mysql mysql:8.4
```

**Vérifier que le conteneur est actif**
```bash
docker ps -a

CONTAINER ID   IMAGE       COMMAND                  CREATED         STATUS                     PORTS     NAMES
3e840b6e1204   mysql:8.4   "docker-entrypoint.s…"   4 minutes ago   Exited (1) 4 minutes ago             mysql
```

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

**Supprimer le conteneur inactif**
```bash
PS C:\Users\russi> docker rm 3e840b6e1204
3e840b6e1204
PS C:\Users\russi> docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
PS C:\Users\russi>
```

**Lancer un nouveau conteneur MySQL**
```bash
docker run --name mysql -e MYSQL_ROOT_PASSWORD=root -d mysql:8.4
079161eb48121961b9397fb4d4a312c695b7cc253eba61c1a0ee662a9bf8be94
```
**Lancer un conteneur PHPMyAdmin**

```bash
docker run --name phpmyadmin -d --link mysql:db -p 8080:80 phpmyadmin
ea4f44eeeb19fee96d9cf64dcb3ba2e1341c5c970e991e5dd5d8cf71bcc34ccd
```
**Visitez l'interface web de PHPMyAdmin**

```bash
curl http://localhost:8080
<!doctype html>
<html lang="en" dir="ltr">
<head>
  <meta charset="utf-8">
```

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


**Lancer la stack compose**

```bash
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu> docker compose up
[+] Running 1/1
 ✔ Container dokerrendu-db-1  Running                                                                                                                                                    0.0s 
Attaching to db-1, pma-1
pma-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.18.0.2. Set the 'ServerName' directive globally to suppress this message
pma-1  | AH00558: apache2: Could not reliably determine the server's fully qualified domain name, using 172.18.0.2. Set the 'ServerName' directive globally to suppress this message
```
**Visitez l'interface Web de PHPMyAdmin**

```bash
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu> curl http://localhost:8080
<!doctype html>
<html lang="en" dir="ltr">
<head>
```

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
**Proposer un nouveau compose.yml**

[Fichier compose modifier](compose.yml)