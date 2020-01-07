
FROM ruby:2.3.3

RUN apt-get update \
    && apt-get install -qq -y \
    build-essential \
    libpq-dev \
    postgresql-client-9.4 \
    ghostscript \
    imagemagick \
    libmagickcore-dev \
    libmagickwand-dev \
    --fix-missing --no-install-recommends
