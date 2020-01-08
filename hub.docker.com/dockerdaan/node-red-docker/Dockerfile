FROM nodered/node-red-docker
USER root
RUN apt update && apt install netcat -y && \
npm install node-red-contrib-tradfri && \
npm install node-red-contrib-homebridge-automation && \
npm install node-red-contrib-sun-position && \
npm install node-red-contrib-timerswitch && \
npm install node-red-contrib-light-scheduler && \
npm install node-red-contrib-telegrambot && \
npm install node-red-contrib-python3-function && \
npm install node-red-contrib-stoptimer && \
npm install node-red-contrib-influxdb
