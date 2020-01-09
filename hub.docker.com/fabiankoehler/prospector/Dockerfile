# -*- docker-image-name: "prospector" -*-
FROM alpine:edge
LABEL maintainer="fkoehler1024@googlemail.com"

# install python3 and pip
RUN apk update && apk add --no-cache curl=7.61.1-r0 python3=3.6.6-r2 python3-dev=3.6.6-r2 gcc=8.2.0-r0 musl-dev=1.1.20-r2 && rm -rf /var/cache/apk/*
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o get-pip.py && /usr/bin/python3 get-pip.py && rm get-pip.py
RUN ln -s /usr/bin/python3 /usr/bin/python

# install prospector
RUN pip install "prospector[with_everything]==1.1.4"
ENTRYPOINT ["/usr/bin/prospector"]
