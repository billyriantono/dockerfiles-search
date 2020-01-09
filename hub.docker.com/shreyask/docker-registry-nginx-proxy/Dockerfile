FROM ubuntu:latest
RUN \
  apt-get update && \
  apt-get install -y vim nano wget build-essential software-properties-common byobu curl git htop man unzip && \
  add-apt-repository -y ppa:nginx/stable && \
  apt-get install -y nginx vim && \
  rm -rf /var/lib/apt/lists/* && \
  chown -R www-data:www-data /var/lib/nginx

# Define mountable directories.
VOLUME ["/etc/nginx/sites-enabled", "/etc/nginx/certs", "/etc/nginx/conf.d", "/var/log/nginx"]

# Define working directory.
WORKDIR /etc/nginx
COPY nginx.conf /etc/nginx/nginx.conf
# Define default command.
CMD ["nginx", "-g", "daemon off;"]

# Expose ports.
EXPOSE 80
