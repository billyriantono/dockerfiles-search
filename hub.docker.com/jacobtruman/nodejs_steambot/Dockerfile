FROM node

RUN npm install nodejs_steambot && \
    mkdir /configs/ && \
    mkdir /logs/ && \
    mkdir /data/ && \
    chmod 777 /configs/ && \
    chmod 777 /logs/ && \
    chmod 777 /data/ && \
    ln -s /configs /node_modules/nodejs_steambot/configs && \
    ln -s /logs /node_modules/nodejs_steambot/logs && \
    ln -s /data /node_modules/nodejs_steambot/data

ENV STEAMBOT_SCRIPT="index.js"

CMD node /node_modules/nodejs_steambot/${STEAMBOT_SCRIPT}
