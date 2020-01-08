#
# MongoDB Dockerfile
#
# https://github.com/dockerfile/mongodb
#

# Pull base image.
FROM ppcelery/dockerfile-base

# supervisord
ADD supervisord.conf /etc/supervisor/supervisord.conf

# Install MongoDB.
RUN \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 && \
    echo "deb http://repo.mongodb.org/apt/ubuntu "$(lsb_release -sc)"/mongodb-org/3.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.0.list && \
    apt-get update && \
    apt-get install -y mongodb-org=3.0.2 && \
    chown -R mongodb:mongodb /var/lib/mongodb && \
    rm -rf /var/lib/apt/lists/*


# Define mountable directories.
VOLUME ["/var/lib/mongodb", "/tmp"]

# Define working directory.
WORKDIR /root

# Expose ports.
EXPOSE 27016
EXPOSE 28016

# Define default command.
# CMD mongod --dbpath=/var/lib/mongodb --storageEngine=wiredTiger
CMD ["supervisord", "-n", "-c", "/etc/supervisor/supervisord.conf"]
