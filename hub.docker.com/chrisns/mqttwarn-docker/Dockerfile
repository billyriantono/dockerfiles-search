FROM python:2.7

MAINTAINER Chris Nesbitt-Smith <chris@cns.me.uk>

ADD https://raw.githubusercontent.com/jpmens/mqttwarn/master/mqttwarn.py /usr/local/bin/mqttwarn.py
RUN pip install paho-mqtt
WORKDIR /opt/mqttwarn

RUN groupadd -r mqttwarn && useradd -r -g mqttwarn mqttwarn && \
  chown -R mqttwarn /opt/mqttwarn /usr/local/bin/mqttwarn.py && \
  chmod +x /usr/local/bin/mqttwarn.py

USER mqttwarn

CMD mqttwarn.py