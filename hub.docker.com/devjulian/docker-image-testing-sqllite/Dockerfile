FROM alpine:3.4
MAINTAINER juliansalas080@gmail.com

##################### INSTALL DEPENDENCIES #######################
RUN apk update && apk add sqlite socat


#################### Run environment variables ########################
ENV SQLDBNAME=testing.db



#################### DirWork #######################

RUN mkdir /db
WORKDIR /db

ENTRYPOINT sqlite3 $SQLDBNAME
