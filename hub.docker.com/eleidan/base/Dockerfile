FROM ubuntu:16.04

LABEL maintainer="Oleg Kulyk" \
      description="Ubuntu 16.04, development base image" \
      init="docker run -it --rm --user $(id -u):$(id -g) -v $(pwd):/home/phantom/app eleidan/base:ubuntu-16.04  docker-init.sh" \
      run="docker run -it --rm --user $(id -u):$(id -g) -v $(pwd):/home/phantom/app eleidan/base:ubuntu-16.04" \
      version="2019-01-16"

ENV SERVICE_NAME="base:ubuntu-16.04"
ENV CONTAINER_PS1="[ $(get_container_ip) | \[\e[0;36m\]$(get_container_service)\[\e[m\] | \[\e[0;35m\]\w\[\e[m\] ]\n\[\e[1;32m\]>\[\e[m\] "
ENV HOME=/home/phantom

COPY .profile .bashrc /etc/skel/
COPY .profile .bashrc /root/

RUN useradd -m -s /bin/bash -u 1000 phantom \
    && mkdir ${HOME}/bash-history/ \
    && touch ${HOME}/bash-history/.bash_history

WORKDIR $HOME

RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends \
        autoconf \
        automake \
        bash-completion \
        bzip2 \
        ca-certificates \
        curl \
        file \
        g++ \
        gcc \
        imagemagick \
        libbz2-dev \
        libc6-dev \
        libcurl4-openssl-dev \
        libdb-dev \
        libevent-dev \
        libffi-dev \
        libgeoip-dev \
        libglib2.0-dev \
        libjpeg-dev \
        liblzma-dev \
        libmagickcore-dev \
        libmagickwand-dev \
        libncurses-dev \
        libpng-dev \
        libpq-dev \
        libreadline-dev \
        libsqlite3-dev \
        libssl-dev \
        libtool \
        libwebp-dev \
        libxml2-dev \
        libxslt-dev \
        libyaml-dev \
        make \
        patch \
        procps \
        tzdata \
        unzip \
        wget \
        xz-utils \
        zlib1g-dev \
        bzr \
        git \
        mercurial \
        openssh-client \
        subversion \
        sudo \
    && rm -rf /var/lib/apt/lists/*

RUN set -ex; \
    if ! command -v gpg > /dev/null; then \
      apt-get update; \
      apt-get install -y --no-install-recommends \
        gnupg2 \
        dirmngr \
      ; \
      rm -rf /var/lib/apt/lists/*; \
    fi


COPY docker-init.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-init.sh

### Needed for the docker-init.sh script
COPY --chown=phantom:phantom recipes $HOME/recipes

RUN chown phantom:phantom -R ${HOME}
RUN echo "phantom ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/phantom

WORKDIR $HOME/app

USER phantom

CMD ["/bin/bash"]
