FROM ruby:2.4.1-slim

RUN apt-get update \
    && apt-get install -y --no-install-recommends --fix-missing \
        build-essential libpq-dev nodejs git openssh-client \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

ENV LANG en_US.UTF-8
ENV HOME /app
ENV APP $HOME
ENV BUNDLE_PATH /gems
ENV BUNDLE_JOBS 4
ENV BUNDLE_RETRY 3

RUN mkdir -p $APP $BUNDLE_PATH

RUN useradd app -s /bin/bash --system
RUN chown -R app.app $APP $BUNDLE_PATH

WORKDIR $APP

# USER app
