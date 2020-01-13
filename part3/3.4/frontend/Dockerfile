FROM node

WORKDIR /app
COPY frontend-example-docker-master frontend-example-docker

RUN useradd -m appuser && chown -R appuser /app

USER appuser

CMD cd frontend-example-docker && npm install && npm start
