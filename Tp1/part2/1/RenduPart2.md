
# 2. Dockerfile
**Récupérez le package.json et app.js que je vous ai cook**

[package](package.json)
[app](./src/app.js)

**Ajoutez un fichier part2/1/Dockerfile**

[Dockerfile](Dockerfile)

**Construire l'image shitty_app à partir de ce Dockerfile**
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1> docker run -p 3000:3000 -d shitty_app:1.0        
b6e910c0a50f99d1fdcdbedf5faae63e8cfa4acf5fd5643ae25c8b15aea4d4db

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
# 3 Hot reload
**Lancer un nouveau conteneur à partir de l'image shitty_app**
``` bash
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1> docker ps     
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1> docker run -p 3000:3000 -d -v "C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1\src:/app/src" shitty_app:1.0
bfc4b1a80a0a976a21c9685c1d52322b17545f9442f541daf630c6c3bb817a27
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1> docker ps                                                             
CONTAINER ID   IMAGE            COMMAND                  CREATED         STATUS         PORTS                                         NAMES
bfc4b1a80a0a   shitty_app:1.0   "docker-entrypoint.s…"   5 seconds ago   Up 4 seconds   0.0.0.0:3000->3000/tcp, [::]:3000->3000/tcp   stupefied_euclid 
  
```

**Vérifier que ça fonctionne**

``` bash
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
# 4. Compose 
**Transformer ce docker run en compose.yml**
``` yaml
services:
  app:
    image: shitty_app:1.0
    ports:
      - "3000:3000"
    volumes:
      - ./src:/app/src
      - ./package.json:/app/package.json
```
``` bash
PS C:\Users\russi\OneDrive\Documents\CoursEfrei\cours docker\DokerRendu\part2\1> docker compose up
Attaching to app-1
Gracefully Stopping... press Ctrl+C again to force
Error response from daemon: failed to set up container networking: driver failed programming external connectivity on endpoint 1-app-1 (633f65f8438c1f82066cd71bda8f7ae1ab580d574b413ac9e692835345194690): Bind for 0.0.0.0:3000 failed: port is already allocated
 
```

# 5. DB

