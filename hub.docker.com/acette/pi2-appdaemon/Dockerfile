FROM resin/raspberry-pi2-python:3.6

EXPOSE 5050

RUN [ "cross-build-start" ]

RUN apt-get update && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
    mkdir -p /usr/src/app

WORKDIR /usr/src/app
VOLUME /conf

# Grab source
RUN git clone https://github.com/home-assistant/appdaemon.git .

# INSTALL
RUN pip3 install . && \
    chmod +x /usr/src/app/dockerStart.sh

CMD [ "./dockerStart.sh" ]

RUN [ "cross-build-end" ]
