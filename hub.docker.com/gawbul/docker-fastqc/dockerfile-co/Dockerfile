FROM node:alpine

RUN	apk update && \
	apk add   bash  && \
	mkdir /data && \
	rm -rf /var/cache/apk/*

COPY data /data

EXPOSE 25
EXPOSE 3000

WORKDIR /data

ENV NODE_PATH=/data/node_modules
RUN npm install --verbose

CMD npm start 
