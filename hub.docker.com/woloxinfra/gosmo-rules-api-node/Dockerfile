FROM node:8.9.4

ADD https://s3.dualstack.us-east-2.amazonaws.com/aws-xray-assets.us-east-2/xray-daemon/aws-xray-daemon-2.x.deb /tmp
RUN cd /tmp/ && \
		apt-get update && \
		apt-get install -y ca-certificates && \
		dpkg -i aws-xray-daemon-2.x.deb && \
		rm aws-xray-daemon-2.x.deb

WORKDIR /home/node/app

COPY package.json .
COPY package-lock.json .
COPY .nvmrc .

RUN npm install

COPY . .

EXPOSE 8080
EXPOSE 2000/udp
ENV NODE_ENV production

RUN chmod a+x entrypoint/start.sh

ENTRYPOINT ["entrypoint/start.sh"]
