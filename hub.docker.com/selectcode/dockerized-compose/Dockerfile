FROM docker

RUN apk add --no-cache openssl bash curl
RUN curl -L --fail https://github.com/docker/compose/releases/download/1.24.0/run.sh -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose