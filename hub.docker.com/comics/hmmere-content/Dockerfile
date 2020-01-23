FROM python:3.6.5

RUN apt-get update && apt-get upgrade -y && \
    rm -f /var/cache/apk/* && \
    python3.6 -m pip install awscli --no-cache-dir
