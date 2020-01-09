FROM python:3-alpine

ENV WEB_CONCURRENCY=4 \
    LISTENING_PORT=8000

ADD . /httpbin

RUN apk add -U ca-certificates libffi libstdc++ && \
    apk add --virtual build-deps build-base libffi-dev && \
    # Pip
    pip install --no-cache-dir gunicorn /httpbin && \
    # Cleaning up
    apk del build-deps && \
    rm -rf /var/cache/apk/*


CMD gunicorn -b 0.0.0.0:${LISTENING_PORT} httpbin:app
