FROM alpine:3.6
ENV AWSCLI_VERSION "1.16.83"
RUN apk -v --update add \
        python \
        py-pip \
        groff \
        less \
        mailcap \
        make \
        && \
    pip install --upgrade pip && \
    pip install --upgrade awscli==${AWSCLI_VERSION} && \
    apk -v --purge del py-pip && \
    rm /var/cache/apk/*
VOLUME /root/.aws