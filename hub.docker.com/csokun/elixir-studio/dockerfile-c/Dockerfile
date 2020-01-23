FROM node:8.8.1

COPY ./ /opt/webserver

RUN cd /opt/webserver && npm install

RUN mv -f /opt/webserver/config/env.prod.cloud.js /opt/webserver/config/env.js

EXPOSE 3000

CMD ["node", "/opt/webserver/index.js"]

