FROM clojure:lein-2.6.1

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list
RUN apt-get update
RUN apt-get -y install google-chrome-beta

# Borrowed from PhantomJS Docker file and trimmed
# Ref https://hub.docker.com/r/wernight/phantomjs/~/dockerfile/
RUN apt-get install -y --no-install-recommends \
        ca-certificates \
        bzip2 \
        libfontconfig

RUN set -x  \
    # Install official PhantomJS release
 && apt-get update \
 && apt-get install -y --no-install-recommends curl \
 && mkdir /tmp/phantomjs \
 && curl -L https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2 \
        | tar -xj --strip-components=1 -C /tmp/phantomjs \
 && mv /tmp/phantomjs/bin/phantomjs /usr/local/bin
 