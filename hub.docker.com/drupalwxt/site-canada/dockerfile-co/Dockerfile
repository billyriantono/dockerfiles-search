FROM ubuntu:18.04

# Install NodeJS and homebridge
RUN apt-get update -y && \
    apt-get install curl -y && \
    curl -sL https://deb.nodesource.com/setup_12.x | bash - && \
    apt-get install -y nodejs && \
    apt-get install -y libavahi-compat-libdnssd-dev && \
    npm install -g --unsafe-perm homebridge && \
    mkdir -p /root/.homebridge && touch /root/.homebridge/config.json

# Install required Plugins
RUN npm install -g homebridge-pilight && \
    npm install -g homebridge-unifi-occupancy-sensor && \
    npm install -g homebridge-http-switch && \
    npm install -g homebridge-http-motion-sensor && \
    npm install -g homebridge-httptemperaturehumidity

# Run homebridge
CMD [ "homebridge" ]