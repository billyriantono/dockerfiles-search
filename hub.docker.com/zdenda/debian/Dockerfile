# Debian with Vim, Git, cURL, Wget, ...

FROM zdenda/git

MAINTAINER Zdenda Kořán <zkoran@gmail.com>

RUN apt-get update \
      && apt-get install -y --no-install-recommends \
        vim \
        bash-completion \
        locales \
      && rm -rf /var/lib/apt/lists/*

# copy default .bashrc to home directory (colors, bash completition, ...)
RUN cp /etc/skel/.bashrc ~/

# setup utf-8
RUN locale-gen C.UTF-8 && \
      /usr/sbin/update-locale LANG=C.UTF-8

ENV LANG C.UTF-8

