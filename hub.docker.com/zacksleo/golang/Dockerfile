FROM golang:alpine
RUN apk add curl git build-base dep
RUN go get golang.org/x/lint/golint
RUN curl -L https://github.com/golang-migrate/migrate/releases/download/v4.2.5/migrate.linux-amd64.tar.gz | tar xvz && chmod +x ./migrate.linux-amd64 && mv migrate.linux-amd64 migrate && cp ./migrate /usr/local/bin/