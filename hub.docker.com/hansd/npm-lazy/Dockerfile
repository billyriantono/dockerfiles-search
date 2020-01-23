FROM node:0.10

RUN npm install -g npm-lazy-mirror

ADD launch.sh /
RUN chmod +x /launch.sh

RUN mkdir -p /data/cache /data/config
VOLUME /data/cache

ADD server-config.json /data/config/server-config.json
ADD package-blacklist.json /data/config/package-blacklist.json


EXPOSE 80
EXPOSE 443


CMD ["/bin/bash", "-c", "/launch.sh"]
