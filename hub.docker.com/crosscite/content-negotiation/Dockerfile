FROM phusion/passenger-full:0.9.22
MAINTAINER Martin Fenner "mfenner@datacite.org"

# Set correct environment variables.
ENV HOME /home/app
ENV DOCKERIZE_VERSION v0.2.0

# Allow app user to read /etc/container_environment
RUN usermod -a -G docker_env app

# Use baseimage-docker's init process.
CMD ["/sbin/my_init"]

# Install Ruby 2.3.3
RUN bash -lc 'rvm --default use ruby-2.4.1'

# Update installed APT packages
RUN apt-get update && apt-get upgrade -y -o Dpkg::Options::="--force-confold" && \
    apt-get install ntp wget tzdata -y && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# install dockerize
RUN wget https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz && \
    tar -C /usr/local/bin -xzvf dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz

# Remove unused SSH service
RUN rm -rf /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh

# Enable Passenger and Nginx and remove the default site
# Preserve env variables for nginx
RUN rm -f /etc/service/nginx/down && \
    rm /etc/nginx/sites-enabled/default && \
    rm /etc/nginx/nginx.conf

# send logs to STDOUT and STDERR
RUN ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log

COPY vendor/docker/webapp.conf /etc/nginx/sites-enabled/webapp.conf
COPY vendor/docker/00_app_env.conf /etc/nginx/conf.d/00_app_env.conf
COPY vendor/docker/70_templates.sh /etc/my_init.d/70_templates.sh
COPY vendor/docker/cors.conf /etc/nginx/conf.d/cors.conf

# Use Amazon NTP servers
COPY vendor/docker/ntp.conf /etc/ntp.conf

# Copy webapp folder
COPY . /home/app/webapp/
RUN mkdir -p /home/app/webapp/vendor/bundle && \
    chown -R app:app /home/app/webapp && \
    chmod -R 755 /home/app/webapp

# Install Ruby gems
WORKDIR /home/app/webapp
RUN gem update --system && \
    gem install bundler && \
    /sbin/setuser app bundle install --path vendor/bundle

# Run additional scripts during container startup (i.e. not at build time)
RUN mkdir -p /etc/my_init.d
COPY vendor/docker/80_flush_cache.sh /etc/my_init.d/80_flush_cache.sh

# Expose web
EXPOSE 80
