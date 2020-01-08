FROM alpine:3.6
ENV AWSCLI_VERSION "1.15.46"
RUN apk -v --update add \
        bash \
        python \
        py-pip \
        groff \
        less \
        mailcap \
        curl \
        jq \
        && \
    pip install --upgrade awscli==${AWSCLI_VERSION} && \
    apk -v --purge del py-pip && \
    rm /var/cache/apk/*
ENTRYPOINT ["aws"]
