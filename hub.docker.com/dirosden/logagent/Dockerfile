FROM gliderlabs/logspout:master
ENV KAFKA_COMPRESSION_CODEC snappy

# - Install basic packages
# - Install supervisord

RUN apk update && \
    apk add wget && \
    apk add curl && \
    apk add supervisor

# Configure Supervisor    
RUN mkdir -p /etc/supervisor.d && \
    mkdir -p /var/log/supervisor
ADD etc	     /etc 
ADD config   /config

# Install Rancher-Gen for Dynamic Config Generation    
RUN wget --no-check-certificate -O /usr/bin/rancher-gen.tar.gz https://github.com/janeczku/go-rancher-gen/releases/download/v0.2.0/rancher-gen-linux-amd64.tar.gz && \
    cd /usr/bin && \
    tar -xzvf rancher-gen.tar.gz && \
    chmod a+x /usr/bin/rancher-gen && \
    rm -f /usr/bin/rancher-gen.tar.gz

# Configure Rancher-Gen
ADD /mnt     /mnt
RUN mkdir -p /mnt/routes

# Expose volumes
VOLUME ["/var/log/supervisor"]

# Exposing Proxy ports
EXPOSE 80

RUN ["chmod", "+x", "/bin/logspout"]
RUN ["chmod", "+x", "/usr/bin/rancher-gen"]
RUN ["chmod", "+x", "/config/bootstrap.sh"]

#Running the Start Script
ENTRYPOINT ["/config/bootstrap.sh"]
