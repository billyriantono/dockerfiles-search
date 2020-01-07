FROM python:3.6-alpine3.7

# update apk repo
RUN echo "http://dl-4.alpinelinux.org/alpine/v3.7/main" >> /etc/apk/repositories && \
    echo "http://dl-4.alpinelinux.org/alpine/v3.7/community" >> /etc/apk/repositories && \
    apk update && \
    apk add chromium chromium-chromedriver libpq postgresql-dev git build-base bash curl sqlite && \
    pip install pipenv

