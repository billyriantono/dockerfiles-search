# includes setuptools and wheel
FROM python:3.6-slim-stretch

MAINTAINER James <j@mesway.io>

ENV PIPENV_VENV_IN_PROJECT true
ENV APP_PATH /code
ENV PATH $APP_PATH:$PATH

# scrapy and selenium
RUN BUILD_DEPS='autoconf \
                build-essential \
                git \
                libssl-dev' \
    && apt-get update \
    && apt-get install -yqq $RUN_DEPS $BUILD_DEPS --no-install-recommends \
    && pip install --upgrade pip \
    && pip install pipenv \
    && apt-get purge -y --auto-remove $BUILD_DEPS \
    && rm -rf /var/lib/apt/lists/*

WORKDIR $APP_PATH

ENTRYPOINT ["pipenv"]
