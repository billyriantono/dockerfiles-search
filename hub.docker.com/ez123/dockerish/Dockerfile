FROM docker:stable

RUN \
    echo "===> Updating TLS certificates..."         && \
    apk --update add \
            ca-certificates \
            openssl \
    && \
    \
    echo "===> Adding usefull packages for devops shell-works..."  && \
    apk --update add \
            coreutils \
            file \
            bash \
            less \
            nano \
            \
            curl \
            wget \
            \
            git \
            make \
            \
            py-pip \
            \
    && \
    pip install docker-compose \
    && \
    echo "===> Cleaning up ..."  && \
    rm -rf \
      "${HOME}/.cache" \
       /var/cache/apk/* \
       /tmp/*               \
       /var/tmp/*           \
    && \
    \
    echo "OK!"

RUN \
  docker --version && \
  docker-compose --version && \
  git --version

