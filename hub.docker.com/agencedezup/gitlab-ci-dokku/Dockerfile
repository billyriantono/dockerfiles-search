FROM alpine:3.6

RUN apk add --no-cache bash git openssh-client

ADD git-push /usr/local/bin/
ADD create-app /usr/local/bin/
ADD provision-service /usr/local/bin/
ADD mount-storage /usr/local/bin/
