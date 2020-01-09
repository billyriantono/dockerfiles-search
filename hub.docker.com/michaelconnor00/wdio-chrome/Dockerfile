FROM node:8-slim
RUN node --version && npm --version

# auto validate license
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections

# update repos
RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee /etc/apt/sources.list.d/webupd8team-java.list
RUN echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu trusty main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886

RUN apt-get update
RUN apt-get install -y --force-yes \
    xvfb \
    build-essential \
    libssl-dev \
    libffi-dev \
    python-dev \
    python \
    oracle-java8-installer

ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# Another layer for smaller more frequent changes, so the above isn't invalidated
RUN apt-get install -y \
    zip \
    psmisc

# Install Chrome driver
RUN wget -N --quiet https://chromedriver.storage.googleapis.com/2.30/chromedriver_linux64.zip && \
    unzip chromedriver_linux64.zip && \
    chmod 755 chromedriver && \
    mv -f chromedriver /usr/local/share/chromedriver && \
    ln -s /usr/local/share/chromedriver /usr/local/bin/chromedriver && \
    ln -s /usr/local/share/chromedriver /usr/bin/chromedriver

# Install Firefox driver
RUN wget -N --quiet https://github.com/mozilla/geckodriver/releases/download/v0.18.0/geckodriver-v0.18.0-linux64.tar.gz #
RUN tar -xzvf geckodriver-v0.18.0-linux64.tar.gz #
RUN chmod 755 geckodriver #
RUN mv -f geckodriver /usr/local/share/geckodriver #
RUN ln -s /usr/local/share/geckodriver /usr/local/bin/geckodriver #
RUN ln -s /usr/local/share/geckodriver /usr/bin/geckodriver

# Install Chrome
RUN wget --quiet https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN dpkg -i google-chrome-stable_current_amd64.deb; apt-get -fy install

# Install node packages
WORKDIR /home/node
RUN npm install --silent \
    webdriverio \
    wdio-mocha-framework \
    wdio-spec-reporter \
    selenium-standalone \
    wdio-selenium-standalone-service

RUN npm install --save-dev wdio-junit-reporter
