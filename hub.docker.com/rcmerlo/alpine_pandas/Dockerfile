FROM python:3.7-alpine3.8
RUN apk --update add --no-cache libstdc++
RUN \
apk add --no-cache --virtual .build-deps g++ && \
pip3 install pycrypto==2.6.1 pandas==0.23.4 && \
apk del .build-deps