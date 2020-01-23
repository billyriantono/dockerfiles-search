FROM maven:3.5-jdk-8-alpine
MAINTAINER Alex Senger <alexander.senger@hu-berlin.de>

RUN echo http://dl-cdn.alpinelinux.org/alpine/edge/testing >> /etc/apk/repositories &&\
	echo http://dl-cdn.alpinelinux.org/alpine/edge/community >> /etc/apk/repositories &&\
	apk update &&\
	apk add g++ &&\
	apk add gcc &&\
	apk add make &&\
	apk add cmake &&\
    apk add openblas-dev &&\
    apk add python3 &&\
    apk add python3-dev &&\
    apk add py3-pip &&\
    apk add py3-psycopg2 &&\
    pip3 install --upgrade pip &&\
    pip3 install scipy && \
    pip3 install numpy &&\
    pip3 install setuptools &&\
    pip3 install pandas &&\
    pip3 install scikit-learn
