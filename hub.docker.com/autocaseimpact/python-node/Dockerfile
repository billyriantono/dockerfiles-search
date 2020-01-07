FROM python:3.6-alpine3.8

RUN apk update; apk add gcc g++ make libffi-dev linux-headers

# Install PostgreSQL
RUN apk --no-cache add postgresql postgresql-dev

# Install Node.js
RUN apk --no-cache add nodejs=8.11.4-r0 npm=8.11.4-r0

# Bower needs git installed
RUN apk --no-cache add git

# Install Chrome
RUN apk add chromium
WORKDIR /usr/src/app
ENV CHROME_BIN=/usr/bin/chromium-browser \
    CHROME_PATH=/usr/lib/chromium/
