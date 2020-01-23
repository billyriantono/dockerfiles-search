FROM python:3.5-alpine

ARG DUMB_INIT_VERSION=1.2.1
ARG SECRETARY_VERSION=0.11.2

COPY entrypoint.sh checker.py requirements.txt img-checker.sh /

RUN apk add --no-cache openssl openssh-client git bash && \
    wget -O /usr/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v${DUMB_INIT_VERSION}/dumb-init_${DUMB_INIT_VERSION}_amd64 && \
    wget -O /usr/bin/secretary https://github.com/ocraviotto/secretary/releases/download/${SECRETARY_VERSION}/secretary-Linux-x86_64 && \
    mv /checker.py /usr/bin/checker.py && \
    mv /img-checker.sh /usr/bin/img-checker && \
    pip install -r /requirements.txt && \
    chmod +x /entrypoint.sh \
        /usr/bin/secretary \
        /usr/bin/dumb-init \
        /usr/bin/checker.py \
        /usr/bin/img-checker && \
    apk del openssl && \
    rm -rf /var/cache/apk/*

ENTRYPOINT ["/entrypoint.sh"]
CMD ["img-checker", "-d", "./"]
