FROM ubuntu:16.04 

WORKDIR /back
COPY backend-example-docker backend-example-docker
RUN apt-get update && apt-get install -y curl nodejs && curl -sL https://deb.nodesource.com/setup_10.x | bash && apt install -y nodejs
RUN node -v && npm -v
ENV FRONT_URL=http://localhost:5000
CMD cd backend-example-docker && npm install && npm start
