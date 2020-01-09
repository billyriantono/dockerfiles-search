FROM node

RUN apt-get update && apt-get install python fontconfig \
  	&& mkdir -p /usr/share \
	&& cd /usr/share \
	&& wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2 \
	&& tar xf phantomjs-2.1.1-linux-x86_64.tar.bz2 && cp -p phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin/phantomjs \
	&& rm -R phantomjs-2.1.1-linux-x86_64* && cd / \
	&& npm install -g casperjs

ENTRYPOINT [ "casperjs" ]
