# Nginx Dockerfile
#
# https://github.com/blackrobot/docker-nginx

FROM damon/base

# Install Nginx.
RUN add-apt-repository -y ppa:nginx/stable
RUN apt-get update -qq && \
    DEBIAN_FRONTEND=noninteractive apt-get install -qqy nginx
RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf

# Attach volumes.
VOLUME /etc/nginx
VOLUME /var/log/nginx

# Set working directory.
WORKDIR /etc/nginx

# Expose ports
EXPOSE 80
EXPOSE 443

# Define default command.
CMD ["nginx"]
