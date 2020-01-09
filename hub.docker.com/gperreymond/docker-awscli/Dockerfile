FROM alpine:3.7

RUN apk --no-cache add --update py-pip bash git openssh-client curl jq && \
    pip install --no-cache-dir --upgrade awscli && \
    curl -L -o /tmp/docker.tgz https://download.docker.com/linux/static/stable/x86_64/docker-17.12.0-ce.tgz && \
    tar -xz -C /tmp/ -f /tmp/docker.tgz && \
    mv /tmp/docker/* /usr/bin && \
    rm -rf /tmp/*

CMD aws
