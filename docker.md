* Exec `docker` command without root
```shell
$ sudo groupadd docker
$ sudo gpasswd -a $USER docker
$ sudo reboot 0
```

* Add insecure registory  
1. Add `daemon.json` file in `/etc/docker`
```json
{
  "insecure-registries" : ["http://10.0.0.131:5000"]
}
```
2. Restart `docker` daemon

* Login Docker Registry
`docker login -u $DOCKER_REG_USER -p $DOCKER_REG_PASS http://$DOCKER_REG_URL`  

* Build Docker image
`docker build -t hello-world-nginx:v1 .` 

* Push Docker image
```shell
export APP_NAME=<application name>
export DOCKER_REG_URL=<Registory host IP:Port>
export IMAGE_TAG_ID=<tag-id>
# confrim `Container ID` by `docker ps`
$ docker commit 792fa27da7dc $APP_NAME
$ docker tag $APP_NAME $DOCKER_REG_URL/$APP_NAME:<$IMAGE_TAG_ID>
$ docker push $DOCKER_REG_URL/$APP_NAME:$IMAGE_TAG_ID
```

