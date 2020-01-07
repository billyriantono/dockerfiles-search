# Pull from Nginx 1.7.11.
FROM nginx:1.7.11

MAINTAINER Greg Werner <werner.greg@gmail.com>


# Install wget and install/updates certificates
RUN apt-get update \
 && apt-get install -y -q --no-install-recommends \
    ca-certificates \
    wget \  
    nano \
    net-tools \
 && rm -r /var/lib/apt/lists/*

# Forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

# Remove the default Nginx configuration file
RUN rm -v /etc/nginx/nginx.conf

# Copy a configuration file from the current directory
ADD nginx.conf /etc/nginx/

# Expose ports.
EXPOSE 80
EXPOSE 443