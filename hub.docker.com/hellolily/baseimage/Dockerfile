FROM alpine:3.8
LABEL maintainer=HelloLily

ENV ALPINE_VERSION=3.8

ENV PACKAGES="\
  musl \
  linux-headers \
  build-base \
  bash \
  ca-certificates \
  python2 \
  python2-dev \
  py-setuptools \
  postgresql-dev=10.5-r0 \
  libxml2-dev \
  libxslt-dev \
  ncurses5-libs \
  nodejs \
  libjpeg-turbo-dev \
  git \
  openssh-client \
  libffi-dev \
  libmaxminddb \
  apk-tools \
"

RUN echo \
  # Add the repository.
  && echo "http://dl-cdn.alpinelinux.org/alpine/v$ALPINE_VERSION/main/" > /etc/apk/repositories \
  # Install the packages (with failsafe).
  && apk add --no-cache $PACKAGES || (sed -i -e 's/dl-cdn/dl-4/g' /etc/apk/repositories && apk add --no-cache $PACKAGES) \
  # Make some useful symlinks that are expected to exist.
  && if [[ ! -e /usr/bin/python ]];        then ln -sf /usr/bin/python2.7 /usr/bin/python; fi \
  && if [[ ! -e /usr/bin/python-config ]]; then ln -sf /usr/bin/python2.7-config /usr/bin/python-config; fi \
  && if [[ ! -e /usr/bin/easy_install ]];  then ln -sf /usr/bin/easy_install-2.7 /usr/bin/easy_install; fi \
  # Install and upgrade Pip.
  && easy_install pip \
  && pip install --upgrade pip \
  && if [[ ! -e /usr/bin/pip ]]; then ln -sf /usr/bin/pip2.7 /usr/bin/pip; fi

# https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/#/add-or-copy
COPY requirements*.txt /

RUN pip install -r /requirements-dev.txt && rm /requirements.txt /requirements-dev.txt

# since we will be "always" mounting the volume, we can set this up
CMD ["python"]
