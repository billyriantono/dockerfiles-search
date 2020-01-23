FROM alpine

RUN apk --update --no-cache add bash bzip2-dev ca-certificates libffi-dev ncurses-dev openssl-dev readline-dev sqlite-dev xz && \
  apk --virtual .build-deps add curl git linux-headers build-base && \
  curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer -o /pyenv-installer && \
  touch /root/.bashrc && \
  /bin/ln -s /root/.bashrc /root/.bash_profile && \
  /bin/bash /pyenv-installer && \
  rm /pyenv-installer && \
  echo 'export PYENV_ROOT="$HOME/.pyenv"' >> /etc/profile && \
  echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> /etc/profile && \
  echo 'eval "$(pyenv init -)"' >> /etc/profile && \
  . /etc/profile && \
  cd /root/.pyenv/versions/ && \
  for v in 3.5.5 3.6.5 3.7.0; do \
    pyenv install --verbose ${v} && tar cJf ${v}.tar.xz ${v} && rm -r ${v}; \
  done && \
  apk del .build-deps


RUN mkdir /usr/local/sbin
RUN echo -e '#!/bin/sh\n\n. /etc/profile\n\ncd ${HOME}/.pyenv/versions\n\nfor version in ${@}; do\n  tar xJf ${version}.tar.xz && rm ${version}.tar.xz\ndone\n\npyenv global ${@}\npyenv rehash\n' > /usr/local/sbin/setup-python
RUN chmod 755 /usr/local/sbin/setup-python
