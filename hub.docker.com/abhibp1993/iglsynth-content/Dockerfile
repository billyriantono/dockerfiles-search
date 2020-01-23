FROM node:12
LABEL name="angular-node-chrome"

# Install Chrome
RUN echo 'deb http://dl.google.com/linux/chrome/deb/ stable main' > /etc/apt/sources.list.d/chrome.list
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
       google-chrome-stable \
	&& rm -rf /var/lib/apt/lists/*

ENV CHROME_BIN /usr/bin/google-chrome

# Log versions
RUN set -x \
    && node -v \
    && npm -v \
    && google-chrome --version