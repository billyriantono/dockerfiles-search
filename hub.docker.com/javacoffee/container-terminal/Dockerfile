FROM webratio/nodejs-http-server

COPY . /opt/www

WORKDIR /opt/www
RUN npm install && npm install bower
RUN ./node_modules/bower/bin/bower --allow-root install
