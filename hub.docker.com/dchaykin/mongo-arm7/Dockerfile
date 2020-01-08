FROM resin/rpi-raspbian

RUN apt-get update && apt-get -y dist-upgrade && \
	apt-get install -y --no-install-suggests mongodb && \
	rm -rf /var/lib/apt/lists/* && \
	mkdir -p /data/db

CMD ["mongod"]

EXPOSE 27017
EXPOSE 28017

ENTRYPOINT /usr/bin/mongod
