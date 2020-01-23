FROM ubuntu:18.04

# APT Packages
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get autoremove -y && \
    apt-get install -y \
        nginx \
        curl \
        fail2ban \
        unzip \
        apache2-utils \
        mysql-client \
        iputils-ping \
        nano \
        software-properties-common \
        nginx-extras \
        && \
    add-apt-repository ppa:certbot/certbot && \
        apt-get update && \
        apt-get install -y python-certbot-nginx \
        && \
    rm -rf /var/lib/apt/lists/*

# Add start command
CMD "nginx -g 'daemon off;'"

# Expose HTTP port
EXPOSE 80

# Expose HTTPS port
EXPOSE 443