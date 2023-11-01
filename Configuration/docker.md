# [Docker](https://www.docker.com/)

### Dependencies

```shell
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```

### Docker repository

```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

```shell
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### Update

```shell
sudo apt update
```

### Install

```shell
sudo apt install docker-ce docker-ce-cli containerd.io
```

### Start & Enable

```shell
sudo systemctl start docker
sudo systemctl enable docker
```

## Dockerfile

### NodeJS

```shell
FROM node

WORKDIR /app

COPY package*.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "app.js"]
```

### Apache2

```shell
FROM ubuntu

RUN apt update

RUN apt install -y apache2

RUN apt clean

COPY . /var/www/html

EXPOSE 80

CMD ["apache2ctl", "-D", "FOREGROUND"]
```

## Images

### Build image

```shell
docker build .
```

```shell
docker build -t my-img .
```

```shell
docker build -t my-img:1.0 .
```

### List images

```shell
docker images
```

```shell
docker image ls
```

### Delete images

```shell
docker rmi <image-id | name>
```

```shell
docker image prune
```

## Containers

### Run container

```shell
docker run -dp 80:80 my-img
```

```shell
docker run -dp 80:80 --name my-cnt my-img
```

```shell
docker run -dp 80:80 --name my-cnt --rm my-img
```

```shell
docker run -dp 80:80 --name my-cnt --rm my-img:1.0
```

### List containers

```shell
docker ps -a
```

```shell
docker container ls
```

### Stop containers

```shell
docker stop <container-id | name>
```

### Delete containers

```shell
docker rm <container-id | name>
```

```shell
docker container prune
```