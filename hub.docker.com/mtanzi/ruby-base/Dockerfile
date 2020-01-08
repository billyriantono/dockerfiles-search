FROM mtanzi/ruby:1.9.3-p547

RUN apt-get update

RUN apt-get install build-essential g++ flex bison gperf ruby perl \
  libsqlite3-dev libfontconfig1-dev libicu-dev libfreetype6 libssl-dev \
  libpng-dev libjpeg-dev python libx11-dev libxext-dev freetype* fontconfig

# Phantomjs
RUN mkdir -p /usr/src \
    && cd /usr/src \
    && wget https://github.com/Pyppe/phantomjs2.0-ubuntu14.04x64/raw/master/bin/phantomjs

RUN cp /usr/src/phantomjs /usr/local/bin/phantomjs \
    && chmod a+x /usr/local/bin/phantomjs

CMD /bin/bash
