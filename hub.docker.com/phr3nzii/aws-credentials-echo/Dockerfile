FROM alpine:latest

RUN apk add --no-cache python3 && \
    python3 -m ensurepip && \
    pip3 install --no-cache --upgrade awscli pip

CMD aws sts get-caller-identity