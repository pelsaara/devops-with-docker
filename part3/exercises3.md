# Excercises 3.1-3.8

## 3.1
###### koko ennen

docker images | grep end
```
backend             latest              2df6b0950887        2 minutes ago       379MB
frontend            latest              5146bd695199        7 minutes ago       331MB
```

docker history frontend
```
IMAGE               CREATED              CREATED BY                                      SIZE                COMMENT
5146bd695199        59 seconds ago       /bin/sh -c #(nop)  CMD ["/bin/sh" "-c" "cd f…   0B                  
fcfd1476a1f4        59 seconds ago       /bin/sh -c node -v && npm -v                    0B                  
0cd2d5a92db1        About a minute ago   /bin/sh -c apt-get update && apt-get install…   207MB               
f2d2ae631631        2 minutes ago        /bin/sh -c #(nop) COPY dir:d00b22bdb52df8027…   570kB               
7ca89f4efe0e        2 minutes ago        /bin/sh -c #(nop) WORKDIR /front                0B                  
c6a43cd4801e        3 weeks ago          /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B                  
<missing>           3 weeks ago          /bin/sh -c mkdir -p /run/systemd && echo 'do…   7B                  
<missing>           3 weeks ago          /bin/sh -c set -xe   && echo '#!/bin/sh' > /…   745B                
<missing>           3 weeks ago          /bin/sh -c rm -rf /var/lib/apt/lists/*          0B                  
<missing>           3 weeks ago          /bin/sh -c #(nop) ADD file:f0b8eaa718bc3965b…   123MB  
```

docker history backend
```
IMAGE               CREATED              CREATED BY                                      SIZE                COMMENT
2df6b0950887        13 seconds ago       /bin/sh -c #(nop)  CMD ["/bin/sh" "-c" "cd b…   0B                  
0270dd781510        14 seconds ago       /bin/sh -c #(nop)  ENV FRONT_URL=http://loca…   0B                  
c3f0413249af        14 seconds ago       /bin/sh -c node -v && npm -v                    0B                  
08aee52bccff        15 seconds ago       /bin/sh -c apt-get update && apt-get install…   207MB               
62d71074ec02        About a minute ago   /bin/sh -c #(nop) COPY dir:263ae863b78de3b3a…   48.6MB              
13a8c855b404        About a minute ago   /bin/sh -c #(nop) WORKDIR /back                 0B                  
c6a43cd4801e        3 weeks ago          /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B                  
<missing>           3 weeks ago          /bin/sh -c mkdir -p /run/systemd && echo 'do…   7B                  
<missing>           3 weeks ago          /bin/sh -c set -xe   && echo '#!/bin/sh' > /…   745B                
<missing>           3 weeks ago          /bin/sh -c rm -rf /var/lib/apt/lists/*          0B                  
<missing>           3 weeks ago          /bin/sh -c #(nop) ADD file:f0b8eaa718bc3965b…   123MB       
```

###### koko jälkeen 

docker image ls | grep end1
```
frontend1           latest              f1d3d265dcef        25 seconds ago      274MB
backend1            latest              c4eb50a8b35f        52 seconds ago      322MB
```

docker history frontend
```
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
5146bd695199        17 minutes ago      /bin/sh -c #(nop)  CMD ["/bin/sh" "-c" "cd f…   0B                  
fcfd1476a1f4        17 minutes ago      /bin/sh -c node -v && npm -v                    0B                  
0cd2d5a92db1        17 minutes ago      /bin/sh -c apt-get update && apt-get install…   207MB               
f2d2ae631631        18 minutes ago      /bin/sh -c #(nop) COPY dir:d00b22bdb52df8027…   570kB               
7ca89f4efe0e        18 minutes ago      /bin/sh -c #(nop) WORKDIR /front                0B                  
c6a43cd4801e        3 weeks ago         /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B                  
<missing>           3 weeks ago         /bin/sh -c mkdir -p /run/systemd && echo 'do…   7B                  
<missing>           3 weeks ago         /bin/sh -c set -xe   && echo '#!/bin/sh' > /…   745B                
<missing>           3 weeks ago         /bin/sh -c rm -rf /var/lib/apt/lists/*          0B                  
<missing>           3 weeks ago         /bin/sh -c #(nop) ADD file:f0b8eaa718bc3965b…   123MB  
```

docker history backend
```
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
2df6b0950887        12 minutes ago      /bin/sh -c #(nop)  CMD ["/bin/sh" "-c" "cd b…   0B                  
0270dd781510        12 minutes ago      /bin/sh -c #(nop)  ENV FRONT_URL=http://loca…   0B                  
c3f0413249af        12 minutes ago      /bin/sh -c node -v && npm -v                    0B                  
08aee52bccff        12 minutes ago      /bin/sh -c apt-get update && apt-get install…   207MB               
62d71074ec02        13 minutes ago      /bin/sh -c #(nop) COPY dir:263ae863b78de3b3a…   48.6MB              
13a8c855b404        13 minutes ago      /bin/sh -c #(nop) WORKDIR /back                 0B                  
c6a43cd4801e        3 weeks ago         /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B                  
<missing>           3 weeks ago         /bin/sh -c mkdir -p /run/systemd && echo 'do…   7B                  
<missing>           3 weeks ago         /bin/sh -c set -xe   && echo '#!/bin/sh' > /…   745B                
<missing>           3 weeks ago         /bin/sh -c rm -rf /var/lib/apt/lists/*          0B                  
<missing>           3 weeks ago         /bin/sh -c #(nop) ADD file:f0b8eaa718bc3965b…   123MB               
```


###### frontend Dockerfile
FROM ubuntu:16.04 

WORKDIR /app

COPY frontend-example-docker frontend-example-docker

RUN apt-get update && apt-get install -y curl && \  
    curl -sL https://deb.nodesource.com/setup_10.x | bash && \  
    apt install -y nodejs && \  
    apt-get purge -y --auto-remove curl && \  
    rm -rf /var/lib/apt/lists/*  

CMD cd frontend-example-docker && npm install && npm start

###### backend Dockerfile
FROM ubuntu:16.04 

WORKDIR /app

COPY backend-example-docker backend-example-docker

RUN apt-get update && apt-get install -y curl && \  
    curl -sL https://deb.nodesource.com/setup_10.x | bash && \  
    apt install -y nodejs && \  
    apt-get purge -y --auto-remove curl && \  
    rm -rf /var/lib/apt/lists/*  

ENV FRONT_URL=http://localhost:5000

CMD cd backend-example-docker && npm install && npm start

## 3.2 

docker build -t yle-dl .   
docker run --rm -ti -u=$(id -u):$(id -g) -v "$(pwd)":/out yle-dl https://areena.yle.fi/1-50250467

###### optimized Dockerfile 

FROM alpine:3.9

RUN apk add --no-cache \  
    bash \  
    curl \  
    ffmpeg \  
    gcc \  
    libxml2-dev \  
    libxslt-dev \  
    make \  
    musl-dev \  
    php7 \  
    php7-bcmath \  
    php7-curl \  
    php7-mcrypt \  
    php7-simplexml \  
    py-crypto \  
    py-lxml \  
    py-pip \  
    py-setuptools \  
    python \  
    python2-dev \  
    rtmpdump \  
    tar \  
    wget && \  
    pip install -U pip setuptools youtube_dl yle-dl && \  
    rm -rf /var/cache/apk/*  

ENTRYPOINT ["yle-dl"]

## 3.3


###### Dockerfile frontend
FROM ubuntu:16.04 

WORKDIR /app

COPY frontend-example-docker frontend-example-docker

RUN apt-get update && apt-get install -y curl && \  
    curl -sL https://deb.nodesource.com/setup_10.x | bash && \  
    apt install -y nodejs && \  
    apt-get purge -y --auto-remove curl && \  
    rm -rf /var/lib/apt/lists/*  
    useradd -m app && chown -R app /app

USER app

CMD cd frontend-example-docker && npm install && npm start

###### Dockerfile backend
FROM ubuntu:16.04 

WORKDIR /app

COPY backend-example-docker backend-example-docker

RUN apt-get update && apt-get install -y curl && \  
    curl -sL https://deb.nodesource.com/setup_10.x | bash && \  
    apt install -y nodejs && \  
    apt-get purge -y --auto-remove curl && \  
    rm -rf /var/lib/apt/lists/* && \  
    useradd -m app && chown -R app /app

USER app

ENV FRONT_URL=http://localhost:5000

CMD cd backend-example-docker && npm install && npm start

## 3.4

docker image ls | grep end
```
frontend            latest              f1d3d265dcef        25 seconds ago      274MB
backend             latest              c4eb50a8b35f        52 seconds ago      322MB
```

###### frontend 
FROM node

WORKDIR /app
COPY frontend-example-docker-master frontend-example-docker

RUN useradd -m appuser && chown -R appuser /app

USER appuser

CMD cd frontend-example-docker && npm install && npm start

###### backend
FROM node

WORKDIR /app
COPY backend-example-docker-master backend-example-docker

RUN useradd -m appuser && chown -R appuser /app

USER appuser

ENV FRONT_URL=http://localhost:5000

CMD cd backend-example-docker && npm install && npm start

docker image ls | grep end
```
frontend            latest              f1d3d265dcef        25 seconds ago      909MB
backend             latest              c4eb50a8b35f        52 seconds ago      909MB
```

## 3.5
###### Dockerfile
FROM node as build-stage

WORKDIR /app
COPY frontend-example-docker-master frontend-example-docker
RUN useradd -m appuser && \
    chown -R appuser /app && \
    cd frontend-example-docker && \
    npm install && npm run build

FROM nginx

COPY --from=build-stage /app/frontend-example-docker/dist/ /srv/http/


## 3.6

###### before
ruby                latest              5db1301d24ff        9 minutes ago       1.06GB

FROM ruby:2.6.0

COPY rails-example-project /mydir/rails-example-project  
WORKDIR /mydir/rails-example-project  
RUN apt-get update && apt-get install -y nodejs  
RUN gem install bundler  
RUN bundle install  
RUN rails db:migrate  

CMD rails s

###### after
ruby2               latest              792ec8cac9fa        About a minute ago   1.04GB

FROM ruby:2.6.0 as build

COPY rails-example-project /mydir/rails-example-project 
 
WORKDIR /mydir/rails-example-project  

RUN apt-get update && apt-get install -y nodejs && \
    gem install bundler && \
    bundle install && \
    rails db:migrate && \
    rm -rf /var/lib/apt/lists/* && \ 
    useradd -m app 

USER app

CMD rails s

## 3.7

## 3.8
I'm skipping this exercise. 
