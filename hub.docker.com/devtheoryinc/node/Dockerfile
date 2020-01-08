FROM bitnami/node:10.13.0-debian-9-prod

USER root

# Install prerequisites
RUN apt-get update && \
  apt-get install -y git wget gnupg && \
  npm install -g yarn

# Install dockerize
ENV DOCKERIZE_VERSION v0.6.1
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && \
  tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && \
  rm dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

# Install MySQL v8.0 client & tools
RUN apt-key adv --keyserver pgp.mit.edu --recv-keys 5072E1F5 && \
  echo "deb http://repo.mysql.com/apt/debian stretch mysql-8.0" | tee /etc/apt/sources.list.d/mysql.list && \
  apt-get update && \
  apt-get install -y mysql-community-client=8.0.13-1debian9

# Install MongoDB client & tools
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4 && \
  echo "deb http://repo.mongodb.org/apt/debian stretch/mongodb-org/4.0 main" | tee /etc/apt/sources.list.d/mongodb-org-4.0.list && \
  apt-get update && \
  apt-get install -y mongodb-org-tools && \
  apt-get install -y mongodb-org-shell && \
  rm -rf /var/lib/apt/lists/*


EXPOSE 27017 33060
