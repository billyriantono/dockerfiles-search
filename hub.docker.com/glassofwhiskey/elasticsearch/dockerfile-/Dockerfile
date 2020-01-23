FROM alpine:latest

RUN apk update
RUN apk add wget

LABEL maintainer="Gaurav Kandoi <kandoigaurav@gmail.com>"
RUN wget http://github.com/bbuchfink/diamond/releases/download/v0.9.22/diamond-linux64.tar.gz
RUN tar xzf diamond-linux64.tar.gz 

ENV PATH=/:$PATH
CMD ["diamond"]

## Sample dockerfile created during NSF Cyber Carpentry 2018. Parts taken from the original Diamond dockerfile and lecture notes.
