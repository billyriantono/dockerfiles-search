FROM python:3.7.2-stretch

RUN apt-get update && apt-get upgrade -y && \
    apt-get install -qqy dumb-init && \
    pip install awscli && \
    aws configure set default.s3.signature_version s3v4 && \
    aws configure set default.region eu-west-1 && \
    echo "Etc/UTC" > /etc/timezone && \
    apt-get purge -y unzip \
                    wget && \
    rm -r /var/lib/apt/lists/* && \
    cd /opt && \
    curl -sLO https://github.com/dcoker/biscuit/releases/download/v0.1.3/biscuit-linux_amd64.tgz && \
    tar xzvf biscuit-linux_amd64.tgz && \
    mv biscuit /usr/bin/biscuit && \
    chmod +x /usr/bin/biscuit && \
    rm biscuit-linux_amd64.tgz

COPY files/setup_common.sh /setup_common.sh
COPY files/decrypt_secrets.sh /decrypt_secrets.sh

ENTRYPOINT ["/usr/bin/dumb-init", "--"]
