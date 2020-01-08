FROM alpine:latest

RUN apk add --update --no-cache \
  python3 \
  curl \
  nano && \
  curl -O https://bootstrap.pypa.io/get-pip.py && \
  python3 get-pip.py && \
  pip3 install awscli --upgrade

CMD tail -f /dev/null
