FROM alpine:latest

RUN apk update
RUN apk add --no-cache alpine-sdk python3 lua5.1 lua5.1-dev luarocks5.1 zip
RUN pip3 install --upgrade pip setuptools requests humanize termcolor
RUN USER=root luarocks-5.1 install busted
