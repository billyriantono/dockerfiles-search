#Get base image
FROM golang:1.10-alpine

# Set environment variables.
ENV HOME /root

#Run some commands
RUN apk add --update git make gcc curl musl-dev linux-headers && \
  	git clone https://github.com/ethereumsocial/multi-geth go-ethereum && \
  	(cd go-ethereum && git checkout v1.8.4 && make geth) && \
  	cp go-ethereum/build/bin/geth /usr/local/bin/ && \
  	rm -rf /go-ethereum

RUN apk add --update nodejs nodejs-npm 	&& \
	npm install npm@latest -g

RUN cd /root/ && \
	git clone --depth=1 https://github.com/ethereumsocial/etsc-net-intelligence-api.git && \
    cd etsc-net-intelligence-api && \
    npm install && \
    npm install -g pm2

#Delete installed packages
RUN npm cache clean --force && \
	apk del git go make gcc curl musl-dev linux-headers nodejs-npm  && \
	rm -rf /var/cache/apk/*

ADD files/app.json /root/etsc-net-intelligence-api/app.json
ADD files/startscript.sh /root/startscript.sh

RUN chmod +x /root/startscript.sh
#expose the ports
EXPOSE 8545
EXPOSE 30303
EXPOSE 30303/udp

ENTRYPOINT ["/root/startscript.sh"]
