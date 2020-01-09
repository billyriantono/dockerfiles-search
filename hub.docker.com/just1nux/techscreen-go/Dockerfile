# Use an official Golang runtime as a parent image using Alpine
FROM golang:1.11

# Get Dependencies
RUN go get -u -v github.com/denisenkom/go-mssqldb github.com/gorilla/mux github.com/jinzhu/gorm github.com/ant0ine/go-json-rest/rest

# RUN mkdir -p ~/go/config
RUN mkdir -p /usr/local/go/src/bitbucket.org/iCampusjjc/techscreen-go
COPY ./ /usr/local/go/src/bitbucket.org/iCampusjjc/techscreen-go
WORKDIR /usr/local/go/src/bitbucket.org/iCampusjjc/techscreen-go

EXPOSE 3000
