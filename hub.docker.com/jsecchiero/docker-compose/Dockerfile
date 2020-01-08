FROM alpine:3.4

RUN     apk -U add \
            python \
            py-pip

RUN     pip install 'docker-compose==1.9.0' && \
        mkdir /data

WORKDIR /data

ENTRYPOINT ["docker-compose"]
