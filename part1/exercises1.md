# Excercises 1.1-1.17

## 1.1
###### docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS                      PORTS               NAMES
6e89e1e19d24        mongo               "docker-entrypoint.s…"   About a minute ago   Exited (0) 32 seconds ago                       fervent_mestorf  
d28a0af162dd        postgres            "docker-entrypoint.s…"   21 minutes ago       Exited (0) 22 seconds ago                       zealous_khorana  
e56028896844        nginx               "nginx -g 'daemon of…"   24 minutes ago       Up 24 minutes               80/tcp              adoring_morse  


## 1.2
###### docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES  

###### docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE  


## 1.3
Give me the **password**: basics   
You found the correct password. **Secret message** is:   
"This is the secret message"  

## 1.4
**docker run -d devopsdockeruh/exec_bash_exercise**  
**docker container ls**  
**docker exec peaceful_curie tail -f ./logs.txt**  
Secret message is:  
"Docker is easy"  

## 1.5
docker run -it -d --name ubulu ubuntu:16.04 sh -c 'echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'  
docker start ubulu  
docker exec ubulu apt-get update  
docker exec ubulu apt-get install -y curl wget  
docker attach ubulu  
helsinki.fi  
Searching..  
```
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>
</body></html>
```


## 1.6 

###### Dockerfile 
FROM devopsdockeruh/overwrite_cmd_exercise

CMD ["-c"]

###### commands
docker build -t docker-clock .  
docker run docker-clock

## 1.7
###### Dockerfile 
FROM ubuntu:16.04 

RUN apt-get update && apt-get install -y curl 

CMD echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;

###### commands
 docker build -t curler .  
docker run -it curler  
Input website:  
helsinki.fi  
Searching..  
```
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">  
<html><head>  
<title>301 Moved Permanently</title>  
</head><body>  
<h1>Moved Permanently</h1>  
<p>The document has moved <a href="http://www.helsinki.fi/">here</a>.</p>  
</body></html>  
```

## 1.8
docker run devopsdockeruh/first_volume_exercise  
contol +c  
docker cp "4b18://usr/app" .  
docker run -v $(pwd):/mydir/usr/app devopsdockeruh/first_volume_exercise  
cat app/logs.txt   
Wed, 08 Jan 2020 10:07:09 GMT  
Wed, 08 Jan 2020 10:07:12 GMT  
Wed, 08 Jan 2020 10:07:15 GMT  
Wed, 08 Jan 2020 10:07:18 GMT  
Secret message is:  
"Volume bind mount is easy"  
Wed, 08 Jan 2020 10:07:24 GMT  

## 1.9

 docker r -p 4000:80 devopsdockeruh/ports_exercise

> ports_exercise@1.0.0 start /usr/app  
> node index.js

Listening on port 80, this means inside of the container. Use -p to map the port to a port of your local machine.

http://localhost:4000/:  
Ports configured correctly!!

## 1.10
###### commands
docker build -t frontend .  
docker run -p 5000:5000 frontend  
Exercise 1.10: Congratulations! You configured your ports correctly!

###### Dockerfile
FROM ubuntu:16.04 

WORKDIR /front  
COPY frontend-example-docker frontend-example-docker  
RUN apt-get update && apt-get install -y curl nodejs && curl -sL   https://deb.nodesource.com/setup_10.x | bash && apt install -y nodejs
RUN node -v && npm -v  
RUN cd frontend-example-docker && npm install  

CMD cd frontend-example-docker && npm start  

## 1.11
###### commands
docker build -t backend .  
docker run -p 8000:8000 -v $(pwd)/backend-example-docker:/back/backend-example-docker backend  
Port configured correctly, generated message in logs.txt
1/8/2020, 12:26:04 PM: Connection received in root  
1/8/2020, 12:26:05 PM: Connection received in root  
Stop -> run
1/8/2020, 12:27:09 PM: Connection received in root  
1/8/2020, 12:27:10 PM: Connection received in root  

###### Dockerfile
FROM ubuntu:16.04 

WORKDIR /back  
COPY backend-example-docker backend-example-docker  
RUN apt-get update && apt-get install -y curl nodejs && curl -sL https://deb.nodesource.com/setup_10.x | bash && apt install -y nodejs
RUN node -v && npm -v  

CMD cd backend-example-docker && npm install && npm start  

## 1.12

###### commands
docker build -t frontend .  
docker run -it -p 5000:5000 frontend  

docker build -t backend .  
docker run -p 8000:8000 -v $(pwd)/backend-example-docker:/back/backend-example-docker backend  

###### Dockerfile front
FROM ubuntu:16.04 

WORKDIR /front  
COPY frontend-example-docker frontend-example-docker  
RUN apt-get update && apt-get install -y curl nodejs && curl -sL https://deb.nodesource.com/setup_10.x | bash && apt install -y nodejs
RUN node -v && npm -v  
ENV API_URL=http://localhost:8000

CMD cd frontend-example-docker && npm install && npm start

###### Dockerfile back 
FROM ubuntu:16.04 

WORKDIR /back  
COPY backend-example-docker backend-example-docker  
RUN apt-get update && apt-get install -y curl nodejs && curl -sL https://deb.nodesource.com/setup_10.x | bash && apt install -y nodejs
RUN node -v && npm -v  
ENV FRONT_URL=http://localhost:5000  

CMD cd backend-example-docker && npm install && npm start  

## 1.13
###### commands
docker build -t javaspring .   
docker run -it -p 8080:8080 javaspring  
"Press here" -> Success

###### Dockerfile
FROM openjdk:8-slim

COPY spring-example-project /mydir/spring-example-project  
WORKDIR /mydir/spring-example-project  
RUN ./mvnw package  

CMD java -jar ./target/docker-example-1.1.3.jar

## 1.14
###### commands
docker build -t ruby .  
docker run -it -p 3000:3000 ruby  
localhost:3000  
New Press  
Total presses: 3  

Press was successfully created.
 
###### Dockerfile

FROM ruby:2.6.0

COPY rails-example-project /mydir/rails-example-project  
WORKDIR /mydir/rails-example-project  
RUN apt-get update && apt-get install -y nodejs  
RUN gem install bundler  
RUN bundle install  
RUN rails db:migrate  

CMD rails s

## 1.15
[https://hub.docker.com/repository/docker/pelsaara/bookmark-mini-project-exercise]

## 1.16
[https://heroku-example-exercise.herokuapp.com/]

## 1.17

I'm skipping this one.
