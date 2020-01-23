FROM alpine:3.4

# Adds testing package to repositories
# Install needed packages. Notes:
#   * build-base: used so we include the basic development packages (gcc)
#   * python-dev: are used for gevent e.g.
#   * bash: so we can access /bin/bash
RUN echo "@testing http://dl-4.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories \
  && apk add --update --no-cache \
              musl \
              build-base \
              python3 \
              python3-dev \
              bash && \
              rm -rf /var/cache/apk/*

RUN python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip

RUN pip3 install --upgrade pip setuptools

# make some useful symlinks that are expected to exist
RUN cd /usr/bin \
  && ln -sf easy_install-3 easy_install \
  && ln -sf idle3 idle \
  && ln -sf pydoc3 pydoc \
  && ln -sf python3 python \
  && ln -sf python-config3 python-config \
  && ln -sf pip3 pip

# since we will be "always" mounting the volume, we can set this up
CMD python
