FROM node as build-stage

WORKDIR /app
COPY frontend-example-docker-master frontend-example-docker
RUN useradd -m appuser && \
    chown -R appuser /app && \
    cd frontend-example-docker && \
    npm install && npm run build

FROM nginx

COPY --from=build-stage /app/frontend-example-docker/dist/ /srv/http/

