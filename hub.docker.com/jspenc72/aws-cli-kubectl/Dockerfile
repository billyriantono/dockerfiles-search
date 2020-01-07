FROM alpine:3.8
LABEL maintainer "J spenc <jspenc72@gmail.com>"

RUN apk -v --update add \
        python \
        py-pip \
        groff \
        less \
        mailcap \
        && \
    pip install --upgrade awscli==1.14.5 s3cmd==2.0.1 python-magic && \
    apk -v --purge del py-pip && \
    rm /var/cache/apk/*

RUN apk --no-cache add openssl \
    && wget -q -O kubectl https://storage.googleapis.com/kubernetes-release/release/v1.12.0/bin/linux/amd64/kubectl \
    && wget -q -O gomplate https://github.com/hairyhenderson/gomplate/releases/download/v3.0.0/gomplate_linux-amd64-slim \
    && chmod +x kubectl gomplate \
    && mv kubectl gomplate /usr/local/bin

VOLUME /root/.aws
VOLUME /project
WORKDIR /project

ENTRYPOINT ["/bin/sh","-c"]
CMD ["aws", "--version"]
WORKDIR /tmp
