FROM ubuntu:17.04

RUN mkdir workspace
WORKDIR workspace

RUN apt-get update
RUN apt-get install -y curl

WORKDIR ~/

ENV NVM_DIR /usr/local/nvm
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash
ENV NODE_VERSION v8.2.1
RUN /bin/bash -c "source $NVM_DIR/nvm.sh && nvm install $NODE_VERSION && nvm use --delete-prefix $NODE_VERSION"

ENV NODE_PATH $NVM_DIR/versions/node/$NODE_VERSION/lib/node_modules
ENV PATH      $NVM_DIR/versions/node/$NODE_VERSION/bin:$PATH

WORKDIR /workspace

RUN apt-get update
RUN apt-get install -y build-essential

RUN apt-get install -y nginx
RUN apt-get install -y php-fpm
RUN apt-get install -y php-mysql
RUN apt-get install -y php7.0-curl
RUN apt-get install -y php7.0-xml 
RUN apt-get install -y php7.0-mbstring 
RUN apt-get install -y zip
RUN apt-get install -y composer

RUN apt-get install -y mysql-client

RUN mkdir redis
WORKDIR redis
RUN curl -O http://download.redis.io/redis-stable.tar.gz
RUN tar xzf redis-stable.tar.gz
WORKDIR redis-stable
RUN make -j4
RUN make install
WORKDIR ../..
RUN rm -rf redis

# Based on https://github.com/mark-adams/docker-chromium-xvfb/blob/master/images/base/Dockerfile
RUN apt-get install -y xvfb chromium-browser
RUN mv /usr/bin/chromium-browser /usr/bin/chromium 
ADD xvfb-chromium /usr/bin/xvfb-chromium
RUN chmod +x /usr/bin/xvfb-chromium
RUN ln -s /usr/bin/xvfb-chromium /usr/bin/google-chrome
RUN ln -s /usr/bin/xvfb-chromium /usr/bin/chromium-browser

RUN mkdir /selenium
WORKDIR /selenium
RUN curl https://selenium-release.storage.googleapis.com/3.4/selenium-server-standalone-3.4.0.jar -o selenium-server-standalone.jar
RUN apt-get install -y default-jre
RUN curl -O https://chromedriver.storage.googleapis.com/2.31/chromedriver_linux64.zip
RUN unzip chromedriver_linux64.zip
RUN rm chromedriver_linux64.zip

WORKDIR /workspace

RUN apt-get install -y libgconf2-4

RUN apt-get install -y ruby ruby-dev libsqlite3-dev
RUN gem install mailcatcher

RUN apt-get autoremove
RUN apt-get clean
