FROM chialab/php:7.0

# Install NodeJS
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash - \
	&& apt-get install -y nodejs

# Update npm manually cuz it cannot update itself (3 -> 5)
RUN mkdir /root/npm_update \
	&& cd /root/npm_update \
	&& npm install npm \
	&& rm -R /usr/lib/node_modules/npm \
	&& cp -r ./node_modules/npm/ /usr/lib/node_modules/npm/ \
	&& rm -R /root/npm_update
