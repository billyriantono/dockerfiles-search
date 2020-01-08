FROM google/dart

RUN apt-get -y update && apt-get install -y apt-utils

RUN apt-get -y update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        wget \
        curl \
        xvfb \
        chromium

ADD xvfb-chromium /usr/bin/xvfb-chromium
RUN ln -s /usr/bin/xvfb-chromium /usr/bin/google-chrome
RUN ln -s /usr/bin/xvfb-chromium /usr/bin/chromium-browser

ENV PATH="$PATH":"/root/.pub-cache/bin"
RUN pub global activate webdev
