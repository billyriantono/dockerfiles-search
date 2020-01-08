FROM golang:1.12-alpine

RUN mkdir /app
WORKDIR /app
ADD main.go /app/main.go
ADD my.cnf /etc/my.cnf
RUN go build main.go && \
    mv main /usr/bin/backup && \
    rm -rf /app

ENTRYPOINT ["backup"]