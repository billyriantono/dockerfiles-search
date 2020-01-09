FROM wesleycharlesblake/nodejs

WORKDIR /ghost  
COPY config.js /ghost/config.js  
RUN wget -O ghost.zip https://ghost.org/zip/ghost-latest.zip \  
    && unzip ghost.zip \
    && rm ghost.zip \
    && npm install --production \
    && npm cache clean \
    && rm -rf /tmp/npm*

CMD ["npm", "start", "--production"]