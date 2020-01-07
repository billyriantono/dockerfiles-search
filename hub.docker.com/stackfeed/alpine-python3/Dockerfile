FROM stackfeed/alpine:3.7
LABEL vendor=stackfeed

LABEL vendor=StackFeed \
      version_tags="[{{version_tags}}]"

RUN apk add --no-cache --update python3 && \
    python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --upgrade pip setuptools && \
        ln -sf /usr/bin/python3 /usr/bin/python && \
        ln -sf /usr/bin/python3-config /usr/bin/python-config && \
        ln -sf /usr/bin/pydoc3 /usr/bin/pydoc && \
        ln -sf /usr/bin/pip3 /usr/bin/pip && \
    rm -r /root/.cache
