FROM docker:latest

RUN apk add --update \
    python \
    python-dev \
    py-pip \
    build-base \
    curl
    
# RUN curl https://bootstrap.pypa.io/get-pip.py | python
    
RUN rm -rf /var/cache/apk/*

RUN pip install docker-compose
