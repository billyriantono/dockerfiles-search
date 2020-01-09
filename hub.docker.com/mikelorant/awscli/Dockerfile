FROM python:alpine

RUN apk add --no-cache \
      groff \
      less && \
    pip install \
      --no-cache-dir \
      --disable-pip-version-check \
      awscli 

ENTRYPOINT ["/usr/local/bin/aws"]
