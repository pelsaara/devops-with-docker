# Excercises 2.1-2.10

## 2.1
###### docker-compose.yml
version: '3' 

services:   
  first_volume_exercise:   
      image: devopsdockeruh/first_volume_exercise   
      build: .   
      volumes:   
        - ./logs.txt:/usr/app/logs.txt    
      container_name: first-vol   

###### logs
Thu, 09 Jan 2020 12:37:13 GMT  
Thu, 09 Jan 2020 12:37:16 GMT  
Thu, 09 Jan 2020 12:37:19 GMT  
Thu, 09 Jan 2020 12:37:22 GMT  

Note: I'm not quite sure I did this right, I had to create the logs.txt to my file system before it worked. 

## 2.2
####### docker-compose.yml
version: '3'  

services:   
  ports_exercise:   
      image: devopsdockeruh/ports_exercise   
      ports:   
        - 80:80   
      container_name: 2dot1

## 2.3
####### docker-compose.yml
version: '3'

services:  
  frontend:  
      ports:  
        - 5000:5000  
      build: ../../part1/1.10  
      container_name: frontend  
  backend:  
      ports:  
        - 8000:8000  
      build: ../../part1/1.11  
      container_name: backend

## 2.4
docker-compose up -d --scale compute=2  
Press here to test your solution -> Congratulations!

## 2.5
###### docker-compose.yml
version: '3.5'

services:  
  frontend:  
      ports:  
        - 5000:5000  
      build: ../../part1/1.10  
      container_name: frontend2.5  
  backend:  
      ports:  
        - 8000:8000  
      build: ../../part1/1.11  
      environment:  
        - REDIS=redis  
      container_name: backend2.5  
  redis:  
      image: redis  
      ports:   
        - 6379:6379  
      container_name: redis2.5  

Press to test -> Working! It took 0.038 seconds.

## 2.6
###### docker-compose.yml
version: '3.5'

services:  
  frontend:  
      ports:  
        - 5000:5000  
      build: ../../part1/1.10  
      container_name: frontend2.6  
  backend:  
      ports:  
        - 8000:8000  
      build: ../../part1/1.11  
      environment:  
        - REDIS=redis  
        - DB_USERNAME=postgres  
        - DB_PASSWORD=salainensana  
        - DB_NAME=postgres  
        - DB_HOST=postgresdb  
      container_name: backend2.6  
  redis:  
      image: redis  
      ports:   
        - 6379:6379  
      container_name: redis2.6  
  postgresdb:  
    image: postgres  
    restart: unless-stopped  
    environment:  
      POSTGRES_PASSWORD: salainensana  
    container_name: postgresdb  

## 2.7
###### docker-compose.yml
version: '3.5'

services:
  frontend:
      ports:  
        - 3000:3000  
      build: ./ml-kurkkumopo-frontend  
      environment:  
        - API_URL=http://localhost:5000 
      container_name: frontend2.7  
  backend:  
      build: ./ml-kurkkumopo-backend  
      volumes:  
        - model:/src/model
      container_name: backend2.7  
  training:  
      build: ./ml-kurkkumopo-training  
      volumes:   
        - model:/src/model
        - ./imgs:/src/imgs
        - ./data:/src/data
      container_name: training2.7  

volumes:  
  model:

## 2.8
###### docker-compose.yml
version: '3.5'

services:  
  frontend:  
      ports:  
        - 5000:5000
      build: ../../part1/1.10  
      container_name: frontend2.8  
  backend:  
      ports:  
        - 8000:8000
      build: ../../part1/1.11  
      depends_on:  
        - postgresdb
      environment:  
        - REDIS=redis
        - DB_USERNAME=postgres
        - DB_PASSWORD=salainensana
        - DB_NAME=postgres
        - DB_HOST=postgresdb
      container_name: backend2.8  
  redis:  
      image: redis  
      ports:   
        - 6379:6379
      container_name: redis2.8  
  postgresdb:  
      image: postgres  
      restart: unless-stopped  
      environment:  
        POSTGRES_PASSWORD: salainensana
      container_name: postgresdb  
  nginx:   
      image: nginx  
      ports:   
        - 80:80
      volumes:  
        - ./nginx.conf:/etc/nginx/nginx.conf
      environment:  
        - NGINX_PORT=80
      container_name: nginx2.8  


## 2.9
###### docker-compose.yml
version: '3.5'

services:  
  frontend:  
      ports:  
        - 5000:5000
      build: ../../part1/1.10  
      container_name: frontend2.6  
  backend:  
      ports:  
        - 8000:8000
      build: ../../part1/1.11  
      depends_on:  
        - postgresdb  
      environment:  
        - REDIS=redis
        - DB_USERNAME=postgres  
        - DB_PASSWORD=salainensana  
        - DB_NAME=postgres  
        - DB_HOST=postgresdb  
      container_name: backend2.6  
  redis:  
      image: redis  
      ports:   
        - 6379:6379  
      container_name: redis2.6  
  postgresdb:  
      image: postgres  
      restart: unless-stopped  
      environment:  
      POSTGRES_PASSWORD: salainensana  
      volumes:  
        - ./postgresdb:/var/lib/postgresql/data  
      container_name: postgresdb  

## 2.10

I'm skipping this one. 
