FROM ubuntu:16.04

# Update, Install Prerequisites
RUN apt-get -y update && \
    apt-get install -y wget perl gcc g++ make automake libtool autoconf \
        m4 gcc-multilib language-pack-en-base software-properties-common \
        python-software-properties && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Stage Files
COPY asset/server.properties /server.properties
COPY asset/start.sh /start.sh
RUN chmod 0755 /start.sh

# Setup container
EXPOSE 19132
VOLUME ["/data"]
WORKDIR /data

COPY asset/pocketmine.yml /pocketmine.yml

# Start Pocketmine
CMD ["/start.sh"]
