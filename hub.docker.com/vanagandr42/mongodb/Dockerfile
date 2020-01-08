FROM vanagandr42/base-debian:8.8-debian-1.19.1.1

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6 \
 && echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/3.4 main" | tee /etc/apt/sources.list.d/mongodb-org-3.4.list \
 && apt-get update \
 && apt-get install -y mongodb-org-server --no-install-recommends \
 && rm -rf /var/lib/apt/lists/* \

# Cleanup
 && rm -rf /tmp/*

# Declare volumes
VOLUME ["/data/db"]

# Add local files
COPY rootfs/ /

# Expose port of the webservice
EXPOSE 27017/tcp
