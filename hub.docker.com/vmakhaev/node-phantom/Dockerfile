FROM rosenhouse/phantomjs2
MAINTAINER Vladimir Makhaev <vmakhaev@gmail.com>

ENV buildDependencies curl

RUN \
  apt-get update && \
  apt-get install -yqq ${buildDependencies} && \
  curl --silent --location https://deb.nodesource.com/setup_4.x | bash - && \
  apt-get install -yqq nodejs && \
  apt-get purge -yqq ${buildDependencies} && \
  apt-get autoremove -yqq && \
  apt-get clean
