FROM node:9.11.1

ENV CHROME_BIN /usr/bin/google-chrome
ENV FIREFOX_BIN /usr/bin/firefox

# Install all the support programs
RUN set -x \
    && echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' > /etc/apt/sources.list.d/chrome.list \
    && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && apt-get update \
    && apt-get install -y pkg-mozilla-archive-keyring bzip2 xvfb google-chrome-stable firefox-esr

# Add the local scripts enabling xvfb
ADD scripts/xvfb-firefox /usr/bin/xvfb-firefox
ADD scripts/xvfb-chrome /usr/bin/xvfb-chrome

# Link and update permissions of scripts
RUN set -x \
    && ln -sf /usr/bin/xvfb-firefox /usr/bin/firefox \
    && ln -sf /usr/bin/xvfb-chrome /usr/bin/google-chrome \
    && chmod +x /usr/bin/xvfb-firefox \
    && chmod +x /usr/bin/xvfb-chrome
