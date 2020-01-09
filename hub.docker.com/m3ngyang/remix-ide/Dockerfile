FROM	node:10.10.0
USER	root
WORKDIR	/home/work/
RUN	apt-get update
RUN	npm install --unsafe-perm --verbose -g remix-ide
RUN	sed -i s/127.0.0.1/0.0.0.0/g /usr/local/lib/node_modules/remix-ide/bin/remix-ide
EXPOSE	8080
EXPOSE	65520
CMD	remix-ide
