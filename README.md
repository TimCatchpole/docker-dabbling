Test 

- build image
```
docker build -f .docker/app.dockerfile -t timtest:1.0 .
```
- -t for tag of image, ease of ref later include version number

- run image
- Linux syntax
```
docker run -d -p 9090:80 -v $(pwd):/var/www/logs -t --name webserver timtest:1.0
```
- Powershell syntax
```
docker run -d -p 9090:80 -v ${PWD}:/var/www/logs --name webserver timtest:1.0
```

- -d for detatched mode, keep console available
- -p for port define host:container set in default
- -v for volume mount a directory on container to host
- -it TTY, terminal to container on run
- --name for defining container name


- Remove all containers
- docker rm -f $(docker ps -aq)

## Docker Compose
```
docker compose up -d --scale tim-test=3
```
- -d detached again
- --scale number of containers to spin up (NOTE: specified port number containers on host.g PORT:3000:8080  web servers can't run at scale, use only for specified port on container e.g PORT:8080)


# Docker Configs & Secrets

- Create config object, dev machine prefixes, publicly accessible settings
```  
docker config create example configs/example.cfg
```
- View config object
```
docker config inspect --pretty example
```
- Create secret object DB u/pws, licence keys etc
```
docker secret create encrypted encrypted.cfg
```
- View secret object
```
docker secret inspect --pretty encrypted
```