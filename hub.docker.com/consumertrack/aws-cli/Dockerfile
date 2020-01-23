FROM alpine:3.9
RUN apk -v --update add \
        python \
        py-pip \
        groff \
        less \
        mailcap \
        zip \
        curl \
        git \
        jq \
        bash \
        openssh-client \
        && \
    pip install --upgrade awscli==1.16.178 s3cmd==2.0.2 python-magic && \
    apk -v --purge del py-pip && \
    rm /var/cache/apk/*
VOLUME /root/.aws
VOLUME /project
WORKDIR /project
CMD ["/bin/sh"]
