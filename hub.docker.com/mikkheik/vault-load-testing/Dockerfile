FROM alpine:3.8

RUN apk update
RUN apk add --update git
RUN apk add --update gcc libc-dev libzmq zeromq-dev
RUN apk add --update python3 python3-dev

RUN git clone https://github.com/hashicorp/vault-load-testing.git
WORKDIR vault-load-testing
RUN pip3 install -r requirements.txt
