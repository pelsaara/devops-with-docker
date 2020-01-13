FROM ubuntu:16.04 

WORKDIR /app

COPY frontend-example-docker frontend-example-docker

RUN apt-get update && apt-get install -y curl && \
    curl -sL https://deb.nodesource.com/setup_10.x | bash && \
    apt install -y nodejs && \
    apt-get purge -y --auto-remove curl && \
    rm -rf /var/lib/apt/lists/* && \
    useradd -m app && chown -R app /app

USER app

CMD cd frontend-example-docker && npm install && npm start
