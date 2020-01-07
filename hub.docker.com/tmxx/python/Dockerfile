FROM alpine:3.3

ENV ALPINE_VERSION 3.3
ENV PYTHON_VERSION 3.5.1-r0
ENV PYTHON_PIP_VERSION 8.1.0

RUN apk --no-cache add \
      ca-certificates \
      libxml2 \
      libxslt \
      python3==$PYTHON_VERSION && \
    apk --no-cache add --virtual build-dependencies \
        curl && \
      curl https://bootstrap.pypa.io/get-pip.py | python3 && \
    apk --no-cache del build-dependencies && \
    pip --no-cache-dir --disable-pip-version-check install -U \
      pip==$PYTHON_PIP_VERSION && \
    ln -s /usr/bin/python3 /usr/bin/python
