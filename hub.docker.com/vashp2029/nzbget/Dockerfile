FROM linuxserver/nzbget

RUN apk add --update --no-cache
RUN apk add --no-cache ffmpeg
RUN apk add --no-cache git
RUN apk add --no-cache py-pip
RUN apk add --no-cache py-openssl
#RUN apk add --no-cache libressl-dev
RUN apk add --no-cache python-dev
RUN apk add --no-cache libffi-dev
RUN apk add --no-cache libxml2-dev
RUN apk add --no-cache libxslt-dev
RUN apk add --no-cache zlib-dev

ENV PYTHONPATH=${PYTHONPATH}:/usr/local/lib/python3.6/site-packages

RUN pip install --upgrade pip
RUN pip install --upgrade setuptools --user python
RUN hash -r pip
RUN pip install --no-binary :all: requests
RUN pip install --no-binary :all: requests[security]
RUN pip install requests-cache
RUN pip install babelfish
RUN pip install 'guessit<2'
RUN pip install 'subliminal<2'
RUN pip install stevedore==1.19.1
RUN pip install python-dateutil
RUN pip install qtfaststart
RUN git clone git://github.com/mdhiggins/sickbeard_mp4_automator.git /sickbeard_mp4_automator/ && \
  touch /sickbeard_mp4_automator/info.log && \
  chmod a+rwx -R /sickbeard_mp4_automator && \
  ln -s /downloads /data && \
  ln -s /config_mp4_automator/autoProcess.ini /sickbeard_mp4_automator/autoProcess.ini && \
  rm -rf \
	/tmp/* \
	/var/lib/apt/lists/* \
	/var/tmp/*

ADD autoProcess.ini /sickbeard_mp4_automator/autoProcess.ini.bak

RUN rm /sickbeard_mp4_automator/autoProcess.ini
RUN mv /sickbeard_mp4_automator/autoProcess.ini.bak /sickbeard_mp4_automator/autoProcess.ini

VOLUME config_mp4_automator
