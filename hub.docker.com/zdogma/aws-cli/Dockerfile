FROM alpine:latest

ARG pip_installer="https://bootstrap.pypa.io/get-pip.py"
ARG awscli_version="1.16.70"

RUN apk --update add \
    python \
    curl \
    groff

RUN curl ${pip_installer} | python && \
    pip install awscli==${awscli_version}

ENTRYPOINT ["/usr/bin/aws"]
CMD ["help"]
