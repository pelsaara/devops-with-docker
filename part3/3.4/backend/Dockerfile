FROM node

WORKDIR /app
COPY backend-example-docker-master backend-example-docker

RUN useradd -m appuser && chown -R appuser /app

USER appuser

ENV FRONT_URL=http://localhost:5000
CMD cd backend-example-docker && npm install && npm start
