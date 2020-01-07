FROM node:6

RUN npm install -g n && n 4.2.1
RUN npm install -g npm@2.14.3
RUN npm install -g bower
RUN npm install -g ember-cli@2.10.0
RUN npm cache clean && bower cache clean --allow-root

# install watchman
RUN \
	git clone https://github.com/facebook/watchman.git &&\
	cd watchman &&\
	git checkout v3.5.0 &&\
	./autogen.sh &&\
	./configure &&\
	make &&\
	make install
  
WORKDIR /var/www/html
