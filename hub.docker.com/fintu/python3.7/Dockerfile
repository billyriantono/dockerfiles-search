FROM python:3.7.3

# Install system dependencies
#
# * libsnappy-dev: for python-snappy
# * gettext-base: for envsubst
RUN apt-get update \
    && apt-get install -y \
        build-essential \
        git \
        libsnappy-dev \
        locales \
        gettext-base \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && echo "de_DE.utf-8 UTF-8" >> /etc/locale.gen \
    && locale-gen

# Set up Poetry et al.
RUN python -m pip install --no-cache-dir poetry mypy codecov tox

# Set up non-root user
RUN mkdir -p /home/app \
    && groupadd -r app && useradd -r -g app -d /home/app app \
    && chown -R app:app /home/app
USER app
WORKDIR /home/app
