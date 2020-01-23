FROM node:12-slim


RUN echo "America/New_York" > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update \
  && apt-get install -yq \
    build-essential libssl-dev autoconf bison libyaml-dev libreadline6-dev \
    zlib1g-dev libncurses5-dev libffi-dev libgdbm3 libgdbm-dev python git \
    software-properties-common apt-transport-https lsb-release ca-certificates \
    gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 \
    libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 \
    libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 \
    libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 \
    ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils wget

RUN git clone https://github.com/rbenv/rbenv.git ~/.rbenv \
  && git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build

COPY .bashrc /root/.bashrc

RUN . ~/.bashrc \
  && rbenv install 2.6.5 \
  && rbenv global 2.6.5

RUN . ~/.bashrc \
  && curl https://packages.sury.org/php/apt.gpg | apt-key add - \
  && echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list \
  && apt-get update \
  && apt-get install -y php7.3

RUN . ~/.bashrc \
  && gem install bundler \
  && mkdir -p /usr/local/share/.cache/bundler \
  && bundle config cache_path /usr/local/share/.cache/bundler


RUN rm /usr/local/bin/yarn \
  && npm i -g yarn \
  && yarn global add elm@0.18.0 elm-format grunt-cli@v1.3.2 bower@1.8.8 codeceptjs@^1.2.1 puppeteer@^1.4.0

WORKDIR /var/www/html

VOLUME /usr/local/share/.cache/bundler
VOLUME /var/www/html/node_modules
VOLUME /var/www/html/elm-stuff
VOLUME /var/www/html/.sass-cache