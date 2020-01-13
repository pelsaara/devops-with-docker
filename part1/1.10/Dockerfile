FROM ubuntu:16.04 

WORKDIR /front
COPY frontend-example-docker frontend-example-docker
RUN apt-get update && apt-get install -y curl nodejs && curl -sL https://deb.nodesource.com/setup_10.x | bash && apt install -y nodejs
RUN node -v && npm -v
ENV API_URL=http://localhost:8000

CMD cd frontend-example-docker && npm install && npm start
