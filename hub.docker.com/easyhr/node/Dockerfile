From node:10.1
LABEL "MAINTAINER" "Kanhai Chhugani"
LABEL "COMPANY" "EasyHR"

RUN echo 'deb http://dl.google.com/linux/chrome/deb/ stable main' > /etc/apt/sources.list.d/chrome.list \
    && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && set -x && apt-get update && apt-get install gettext-base xvfb google-chrome-stable -y \
    && wget -q -O /usr/bin/xvfb-chrome https://bitbucket.org/atlassian/docker-node-chrome-firefox/raw/ff180e2f16ea8639d4ca4a3abb0017ee23c2836c/scripts/xvfb-chrome \
    && ln -sf /usr/bin/xvfb-chrome /usr/bin/google-chrome \
    && chmod 755 /usr/bin/google-chrome \
    && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false $buildDeps \
    && rm -rf /var/lib/apt/lists/* \
    && npm install -g @angular/cli 