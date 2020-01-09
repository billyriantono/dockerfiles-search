FROM debian:jessie

MAINTAINER WHITEPLUS System "sysadmin@wh-plus.com"

ENV PHANTOM_JS_TAG 2.0.0

ENV buildDependencies\
  wget unzip python build-essential g++ flex bison gperf\
  ruby perl libsqlite3-dev libssl-dev libpng-dev

ENV phantomJSDependencies\
  libicu-dev libfontconfig1-dev libjpeg-dev libfreetype6 libqt5webkit5-dev openssl

ENV spiderDependencies\
  python

RUN \
    # Installing dependencies
    apt-get update -yqq \
&&  apt-get upgrade -y \
&&  apt-get install -fyqq ${buildDependencies} ${phantomJSDependencies} ${spiderDependencies}\
    # Downloading src, unzipping & removing zip
&&  mkdir phantomjs \
&&  cd phantomjs \
&&  wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-${PHANTOM_JS_TAG}-source.zip \
&&  unzip phantomjs-${PHANTOM_JS_TAG}-source.zip \
&&  rm -rf /phantomjs/phantomjs-${PHANTOM_JS_TAG}-source.zip \
    # Building phantom
&&  cd phantomjs-${PHANTOM_JS_TAG}/ \
&&  ./build.sh --jobs 1 --confirm --silent \
    # Removing everything but the binary
&&  ls -A | grep -v bin | xargs rm -rf \
    # Symlink phantom so that we are able to run `phantomjs`
&&  ln -fns /phantomjs/phantomjs-${PHANTOM_JS_TAG}/bin/phantomjs /usr/local/share/phantomjs \
&&  ln -fns /phantomjs/phantomjs-${PHANTOM_JS_TAG}/bin/phantomjs /usr/local/bin/phantomjs \
&&  ln -fns /phantomjs/phantomjs-${PHANTOM_JS_TAG}/bin/phantomjs /usr/bin/phantomjs \
    # Removing build dependencies, clean temporary files
&&  apt-get purge -yqq ${buildDependencies} \
&&  apt-get autoremove -yqq \
&&  apt-get clean \
&&  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    # Checking if phantom works
&&  phantomjs -v \
    # Install Python libraries
&&  curl -kL https://raw.github.com/pypa/pip/master/contrib/get-pip.py | python \
&&  pip install selenium scrapy

CMD \
    echo "phantomjs binary is located at /phantomjs/phantomjs-${PHANTOM_JS_TAG}/bin/phantomjs"\
&&  echo "just run 'phantomjs' (version `phantomjs -v`)"