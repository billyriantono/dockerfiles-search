# FROM golang:1.11-alpine as builder
FROM alpine:latest

# get updates and install necessary packages for cicleci
RUN apk update && apk add wget && apk add git && rm -rf /var/cache/apk/*

RUN wget https://github.com/gohugoio/hugo/releases/download/v0.54.0/hugo_0.54.0_Linux-64bit.tar.gz
RUN tar -C /usr/bin -zxf hugo_0.54.0_Linux-64bit.tar.gz
