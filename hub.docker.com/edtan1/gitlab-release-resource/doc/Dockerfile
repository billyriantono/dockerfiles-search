FROM node:10.15.3
RUN apt-get update
RUN apt-get -y install make gcc g++ python redis-server libzmq3-dev
WORKDIR /app
COPY package* /app/
RUN npm install

COPY api /app/api
COPY lib /app/lib
COPY services /app/services
EXPOSE 3001

COPY runtimeInit.sh runtimeInit.sh
COPY cache/redis.conf /usr/local/etc/redis/redis.conf
EXPOSE 6379

CMD ["/bin/bash", "./runtimeInit.sh"]
