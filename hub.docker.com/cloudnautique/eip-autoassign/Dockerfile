FROM alpine

RUN apk add --update python py-pip \
    && pip install aws-ec2-assign-elastic-ip \
    && rm -rf /var/cache/apk/*

COPY ./entrypoint.sh /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
