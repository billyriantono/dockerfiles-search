FROM williamyeh/ansible:alpine3

RUN apk add --update alpine-sdk python-dev git curl \ 
    && pip install apache-libcloud pycrypto ovh \
    && apk del alpine-sdk python-dev
