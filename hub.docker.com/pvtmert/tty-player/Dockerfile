#!/usr/bin/env docker build --compress -t pvtmert/tty-player -f
# docker run --rm -itd -p 80:80 -v $(pwd):/usr/share/nginx/html:ro -d nginx

FROM nginx:latest

WORKDIR /usr/share/nginx/html

RUN rm -rf *

COPY ./ ./
