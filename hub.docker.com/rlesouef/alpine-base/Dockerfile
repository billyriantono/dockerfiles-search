FROM alpine:3.5

MAINTAINER Open Source Services [opensourceservices.fr]

RUN apk --update add \
    bash nano \
    && rm -rf /var/cache/apk/*

COPY src/ .

CMD ["bash"]
