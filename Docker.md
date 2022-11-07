# Docker CheatSheet

## Build image locally
```
docker build -t . <your username>/node-web-app
```

## run it to test
```
docker run -p 49160:8080 -d <your username>/node-web-app
```

## Create a repo and publish to docker hub
```
docker tag mclan/unwrapping-webapp:latest lanboy/vault-webapp-repo:unwrapping-webapp
docker push lanboy/vault-webapp-repo:unwrapping-webapp
```

## Commit changes
```
sudo docker commit [CONTAINER_ID] [new_image_name]
```