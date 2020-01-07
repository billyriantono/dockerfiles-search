FROM r0m1bl/alpine-python

RUN apk add --update git && \
    rm /var/cache/apk/*

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY requirements.txt /usr/src/app/
RUN pip install --no-cache-dir -r requirements.txt

ONBUILD COPY . /usr/src/app