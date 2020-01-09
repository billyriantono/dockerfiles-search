FROM pataquets/ubuntu:xenial

MAINTAINER Paul Podgorsek <ppodgorsek@users.noreply.github.com>
LABEL description Robot Framework in Docker.

VOLUME /opt/robotframework/reports
VOLUME /opt/robotframework/tests

ENV SCREEN_COLOUR_DEPTH 24
ENV SCREEN_HEIGHT 1080
ENV SCREEN_WIDTH 1920

RUN apt-get update\
	&& apt-get install -y\
                libxss1\
                libappindicator1\
                libindicator7\
  gconf-service\
  libasound2\
  libgconf-2-4\
  libnspr4\
  fonts-liberation\
  libnss3\
  lsb-release\
                xdg-utils\
                unzip\
                wget\
                python-pip\
		xvfb\
	&& apt-get autoremove

RUN cd /tmp && wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb\
            && dpkg -i google-chrome*.deb && apt-get install -f

RUN cd /tmp && wget -N http://chromedriver.storage.googleapis.com/2.26/chromedriver_linux64.zip\
            && unzip chromedriver_linux64.zip\
            && chmod +x chromedriver\
            && mv -f chromedriver /usr/local/share/chromedriver\
            && ln -s /usr/local/share/chromedriver /usr/local/bin/chromedriver\
            && ln -s /usr/local/share/chromedriver /usr/bin/chromedriver



RUN pip install --upgrade pip

RUN pip install robotframework==3.0.2\
	robotframework-selenium2library==3.0.0
	
#ADD drivers/geckodriver-v0.19.1-linux64.tar.gz /opt/robotframework/drivers/

COPY bin/chromedriver.sh /opt/robotframework/bin/chromedriver
COPY bin/chromium-browser.sh /opt/robotframework/bin/chromium-browser
COPY bin/run-tests-in-virtual-screen.sh /opt/robotframework/bin/

# FIXME: below is a workaround, as the path is ignored
RUN mv /usr/bin/google-chrome-stable /usr/bin/google-chrome-stable-original\
	&& ln -sfv /opt/robotframework/bin/chromium-browser /usr/bin/google-chrome-stable

ENV PATH=/opt/robotframework/bin:/opt/robotframework/drivers:$PATH

CMD ["run-tests-in-virtual-screen.sh"]
