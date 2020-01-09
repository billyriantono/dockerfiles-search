FROM isaackuang/alpine-base:3.8.0

RUN wget https://github.com/golang-migrate/migrate/releases/download/v4.4.0/migrate.linux-amd64.tar.gz && \
    tar zxvf migrate.linux-amd64.tar.gz && \
    mv migrate.linux-amd64 /bin/migrate && \
    rm -rf migrate.linux-amd64.tar.gz

WORKDIR /data

ENTRYPOINT ["/bin/migrate"]