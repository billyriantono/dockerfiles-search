FROM golang:1.11.5-alpine3.9

RUN apk add --no-cache git mercurial \
    && go get -d -v github.com/gorilla/handlers \
                    github.com/gorilla/mux \
                    gopkg.in/mgo.v2 \
                    gopkg.in/mgo.v2/bson \
                    github.com/google/uuid \
                    github.com/dgrijalva/jwt-go \
                    golang.org/x/crypto/bcrypt \
                    github.com/mikespook/gorbac \
    && apk del git mercurial \