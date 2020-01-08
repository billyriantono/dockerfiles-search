FROM primerevenue/ruby-base:xenial-2.5.1-latest

#Figure out how to remove later
RUN apt-get update --fix-missing && apt-get -y upgrade &&\
  apt-get install -y \
  chromium-chromedriver \
  --no-install-recommends \
  && sleep 3 \
  && ln -s /usr/lib/chromium-browser/chromedriver /usr/bin/chromedriver \
  && ln -s /usr/lib/chromium-browser/chromedriver /usr/bin/chrome-driver


## Install node and yarn
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
  && apt-get install -y nodejs \
  && curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
  echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
  apt-get update && apt-get install yarn
