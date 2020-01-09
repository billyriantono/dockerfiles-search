FROM rosenhouse/phantomjs2
MAINTAINER Lukas Eipert <leipert@users.noreply.github.com>

RUN \
    apt-get update -yqq \
&&  apt-get install -fyqq build-essential curl git \
&&  curl --silent --location https://deb.nodesource.com/setup_4.x | sudo bash - \
&&  apt-get install -fyqq nodejs \
&&  npm install -g gulp bower \
&&  npm cache clean \
&&  apt-get purge -yqq build-essential curl \
&&  apt-get autoremove -yqq \
&&  apt-get clean \
&&  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
&&  phantomjs -v && git --version && node -v && gulp -v && bower -v

CMD \
    echo "phantomjs version: `phantomjs -v`"\
&&  echo "`git --version`"\
&&  echo "node version: `node -v`"\
&&  echo "npm version: `npm -v`"\
&&  echo "gulp version: `gulp -v`"\
&&  echo "bower version:  `bower -v`"
