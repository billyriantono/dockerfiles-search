FROM homeassistant/home-assistant:0.45.1

VOLUME /config

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

RUN echo "deb http://httpredir.debian.org/debian jessie-backports main contrib non-free" | tee -a /etc/apt/sources.list
RUN apt-get update  -y
RUN apt-get install -y apt-utils
RUN apt-get upgrade -y
RUN apt-get install -y -t jessie-backports vlc
RUN apt-get install -y mosquitto-clients
RUN apt-get update  -y

# Copy source
COPY . .

CMD [ "python", "-m", "homeassistant", "--config", "/config" ]
