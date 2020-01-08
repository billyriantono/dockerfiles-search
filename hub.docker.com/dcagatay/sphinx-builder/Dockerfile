FROM python:3.8
MAINTAINER Dogukan Cagatay <dcagatay@gmail.com>

ENV DISPLAY ":0.0"
ENV DEBIAN_FRONTEND "noninteractive"

RUN sh -c 'echo "deb [arch=amd64] http://deb.debian.org/debian buster contrib" >> /etc/apt/sources.list.d/debian-contrib.list' && \
  apt-get update && apt-get install --no-install-recommends --yes \
	curl \
	make \
	supervisor \
	latexmk \
	texlive-fonts-recommended \
	texlive-latex-extra \
  ttf-mscorefonts-installer \
	libgtk-3-0 \
	libnotify4 \
	libnss3 \
	libxtst6 \
	libatspi2.0-0 \
	libappindicator3-1 \
	libsecret-1-0 \
	libasound2 \
	x11vnc \
	xvfb

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
	sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' && \
	apt-get update && apt-get install -y --no-install-recommends google-chrome-stable

RUN curl -Lsq https://github.com/krallin/tini/releases/download/v0.18.0/tini_0.18.0-amd64.deb > /tmp/tini-amd64.deb && \
	dpkg -i /tmp/tini-amd64.deb && \
	rm -rf /tmp/tini-amd64.deb

RUN curl -Lsq https://github.com/jgraph/drawio-desktop/releases/download/v12.1.7/draw.io-amd64-12.1.7.deb > /tmp/draw.io-amd64.deb && \
	dpkg -i /tmp/draw.io-amd64.deb && \
	rm -rf /tmp/draw.io-amd64.deb

COPY entrypoint.sh /entrypoint.sh
COPY conf/supervisord.conf /etc/supervisord.conf

WORKDIR /docs

ENTRYPOINT ["/usr/bin/tini", "--", "/entrypoint.sh"]
CMD ["make", "html"]
