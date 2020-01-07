FROM node:8.15.1-jessie

ENV PM2_INSTANCES=2 \
    PM2_EXEC_MODE="cluster" \
    PM2_SCRIPT="/srv/server.js" \
    PM2_LOG_TYPE="json" \
    PM2_LOG_DATE_FORMAT="YYYY-MM-DD HH:mm:ss" \
    PM2_RESTART_DELAY="4000" \
    PM2_WAIT_READY="false"

RUN apt-get update && \
    apt-get install gettext -y --no-install-recommends && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    npm install -g pm2@3.5.1 && \
    npm install -g yarn@1.19.2 && \
    chmod +x /usr/local/bin/yarn


COPY ./base /base
