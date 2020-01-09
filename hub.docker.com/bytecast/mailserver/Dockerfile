FROM tvial/docker-mailserver:release-v6.1.0

RUN apt-get update -q --fix-missing && \
    apt-get -y upgrade && \
    apt-get -t stretch-backports -y install --no-install-recommends \
      dovecot-mysql \
      postfix-mysql \
      && \
    apt-get autoclean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /usr/share/locale/* && \
    rm -rf /usr/share/man/* && \
    rm -rf /usr/share/doc/* && \
    update-locale

