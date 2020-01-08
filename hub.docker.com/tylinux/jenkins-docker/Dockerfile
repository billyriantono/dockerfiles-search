FROM jenkins/jenkins:alpine

USER root

# RUN echo https://mirrors.ustc.edu.cn/alpine/v3.9/main > /etc/apk/repositories; \
#     echo https://mirrors.ustc.edu.cn/alpine/v3.9/community >> /etc/apk/repositories

# install acme.sh
RUN apk update -f \
  && apk --no-cache add -f \
  openssl \
  coreutils \
  bind-tools \
  curl \
  socat \
  tzdata \
  tar \
  && rm -rf /var/cache/apk/*

ENV LE_CONFIG_HOME /acme.sh

ENV AUTO_UPGRADE 1

RUN wget  -O /tmp/acme.sh.zip https://github.com/Neilpang/acme.sh/archive/2.8.2.zip 
RUN unzip /tmp/acme.sh.zip -d /tmp/ \
    && mv /tmp/acme.sh-2.8.2 /install_acme.sh

#Install
RUN cd /install_acme.sh && ([ -f /install_acme.sh/acme.sh ] && /install_acme.sh/acme.sh --install --home /jenkins/) && rm -rf /install_acme.sh/

RUN chown jenkins:jenkins -R /jenkins/
RUN ln -s /jenkins/acme.sh /usr/local/bin/

# install Python
RUN apk add --no-cache python3 && \
    python3 -m ensurepip && \
    pip3 install --upgrade pip setuptools && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
    if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi && \
    rm -r /root/.cache

# install Node.js, NPM and Yarn
RUN apk add --no-cache nodejs npm && \
    npm install -g yarn

ENV GOSU_VERSION 1.11
RUN set -eux; \
    \
    apk add --no-cache --virtual .gosu-deps \
    dpkg \
    gnupg \
    ; \
    \
    dpkgArch="$(dpkg --print-architecture | awk -F- '{ print $NF }')"; \
    wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch"; \
    wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$dpkgArch.asc"; \
    \
    # verify the signature
    export GNUPGHOME="$(mktemp -d)"; \
    # for flaky keyservers, consider https://github.com/tianon/pgp-happy-eyeballs, ala https://github.com/docker-library/php/pull/666
    gpg --batch --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4; \
    gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu; \
    command -v gpgconf && gpgconf --kill all || :; \
    rm -rf "$GNUPGHOME" /usr/local/bin/gosu.asc; \
    \
    # clean up fetch dependencies
    apk del --no-network .gosu-deps; \
    \
    chmod +x /usr/local/bin/gosu; \
    # verify that the binary works
    gosu --version; \
    gosu nobody true \
    && rm -rf /var/cache/apk/*

#switch to root to run
VOLUME /acme.sh
COPY entrypoint.sh /entrypoint.sh
RUN chmod u+x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
CMD ["jenkins", "/sbin/tini", "--", "/usr/local/bin/jenkins.sh"]
