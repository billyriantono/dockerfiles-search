FROM alpine:latest

# bash is necessary to run env loading scripts
RUN \
    apk update && \
    apk add git python py-pip bash && \
    pip install awsebcli && \
    pip install awscli