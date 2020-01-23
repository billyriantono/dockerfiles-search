FROM delconis/sailsjs

ENV SAILSJS_VERSION=latest

# Install NPM Modules
RUN npm install socket.io-redis@~1.0.0 --save --save-exact
RUN npm install sails-mysql --save
RUN sails new test

# Redist Config Defaults
ENV sails_config_sockets_adapter=socket.io-redis
# Override these
ENV sails_config_sockets_host=127.0.0.1
ENV sails_config_sockets_port=6379
ENV sails_config_sockets_db=sailsjs
ENV sails_config_sockets_pass=pass

#MySQL Config
ENV sails_models__connection=mysqlServer
#Override these
ENV sails_connections__mysqlServer__adapter=sails-mysql
ENV sails_connections__mysqlServer__password=changeme
ENV sails_connections__mysqlServer__user=root
ENV sails_connections__mysqlServer__host=127.0.0.1
ENV sails_connections__mysqlServer__database=sailsjs

WORKDIR /workdir/test
RUN mkdir /workdir/test/.tmp

RUN npm install

EXPOSE 1337
EXPOSE 8080

CMD sails lift




