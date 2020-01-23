FROM fdsa/python-selenium:base

RUN apt-get update && apt-get -y upgrade && \
	apt-get install -y wget

RUN wget -P /tmp/ https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN dpkg -i /tmp/google-chrome-stable_current_amd64.deb; apt-get -fy install

RUN echo 'Chrome location: '`which google-chrome`
