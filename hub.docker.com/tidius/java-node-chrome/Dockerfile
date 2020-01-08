FROM openjdk:11-jre
LABEL name="java-node-chrome"

# Install Chrome

RUN echo 'deb http://dl.google.com/linux/chrome/deb/ stable main' > /etc/apt/sources.list.d/chrome.list

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -

RUN set -x \
    && apt-get update \
    && apt-get install -y \
        google-chrome-stable

ENV CHROME_BIN /usr/bin/google-chrome

# Install node

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -
RUN apt-get update -qqy && apt-get -qqyy install \
    nodejs \
    && rm -rf /var/lib/apt/lists/*

# Log versions

RUN set -x \
    && node -v \
    && npm -v \
    && google-chrome --version \
    && java -version