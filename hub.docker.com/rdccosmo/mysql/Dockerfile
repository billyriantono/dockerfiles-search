FROM mysql:8
RUN apt-get update && apt-get install -y \
    xz-utils \
    && rm -rf /var/lib/apt/lists/*
RUN mkdir /backups

RUN touch /var/lib/mysql/queries.log
COPY ./container-files /
VOLUME /backups
