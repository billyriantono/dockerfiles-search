FROM wisbyme/ubuntu16

LABEL maintainer="ljjun <wisbyme@gmail.com>"

ENV NODEJSVER 12

RUN apt-get update -y \
 && apt-get install -y --no-install-recommends \
    wget curl libssh-dev openssl build-essential \
 && curl -sL https://deb.nodesource.com/setup_${NODEJSVER}.x | bash - \
 && apt-get install -y --no-install-recommends nodejs \
 #&& wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash \
 && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
 && echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list \
 && apt-get update \
 && apt-get install --no-install-recommends yarn \
 && npm install pm2 vue-cli -g \
 && apt-get autoremove -y \
 && apt-get autoclean -y \
 && rm -rf /var/cache/apt/* /var/lib/apt/lists/* /tmp/* /var/tmp/* \
 && /sbin/install_clean

