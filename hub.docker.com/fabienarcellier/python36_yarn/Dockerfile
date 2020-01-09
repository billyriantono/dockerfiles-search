FROM alpine:3.9
MAINTAINER Fabien Arcellier <fabien.arcellier@gmail.com>

RUN apk add yarn &&\
        apk add python3 &&\
        pip3 install virtualenv &&\
        ln -s /usr/bin/python3 /usr/local/bin/python

CMD echo blueprint-dockerhub-automaticbuild
