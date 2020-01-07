FROM alpine:3.8
LABEL maintainer 'sshnaidm <einarum@gmail.com>'
LABEL description 'Python 3 on Alpine Linux 3.8'

RUN apk add --no-cache python3 bash postgresql-dev build-base python3-dev && \
python3 -m ensurepip && \
rm -r /usr/lib/python*/ensurepip && \
pip3 install --upgrade pip setuptools && \
rm -r /root/.cache && \
ln -s /usr/bin/python3 /usr/bin/python
