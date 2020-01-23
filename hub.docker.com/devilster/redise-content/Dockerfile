FROM jenkins
MAINTAINER Mika Puhakka <mika.puhakka@geniem.com>
USER root
# RUN curl -sL https://deb.nodesource.com/setup_7.x | bash /dev/stdin
RUN apt-get update && apt-get install -y \
    xvfb \
    libfontconfig \
    python-pip \ 
    libnss3 \
    unzip 
    # nodejs \

RUN wget https://chromedriver.storage.googleapis.com/2.27/chromedriver_linux64.zip && \
    unzip chromedriver_linux64.zip && \
    chmod 755 chromedriver && \
    mv chromedriver /usr/bin/chromedriver && \
    apt-get remove unzip -y

RUN chmod 755 /usr/bin/chromedriver
RUN pip install robotframework-selenium2library
# RUN npm install -g phantomjs
# RUN apt-get purge firefox
# RUN mkdir -p /etc/legacy_firefox
ENV JAVA_OPTS=-Dhudson.model.DirectoryBrowserSupport.CSP=""
RUN apt-get update && apt-get install -y \
    chromium 
USER jenkins
