FROM michaelpc/openshift:latest

USER 0

ADD scripts /tmp/setup

ADD http://chromedriver.storage.googleapis.com/2.0/chromedriver_linux64.zip /tmp/setup/chromedriver.zip

RUN sh /tmp/setup/install.sh

WORKDIR /app

ENV START_PAGE https://google.com

ENV VNC_PW NbHEnToVJD2lzAv2K6NNPKJii8h6jK

ENV VNC_PORT 5900

ENV VNC_RESOLUTION 1920x1080x24

ENV SELENIUM_PORT 4444

ENV IN_RUN_UNLOCK "rm -fv /app/.config/google-chrome/SingletonLock"

ENV KEEP_RUN_X /usr/local/bin/xserver.sh

ENV KEEP_RUN_VNC /usr/local/bin/vnc.sh

ENV KEEP_RUN_CHROME /usr/local/bin/chrome.pl

ENV DISPLAY :99

ENV XVFB xvfb-run

ENV CONFIG_DIR /app/.config/google-chrome

USER 1000
