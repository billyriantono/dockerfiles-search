# VERSION 1.0
# DOCKER-VERSION  1.2.0
# AUTHOR:         Richard Lee <lifuzu@gmail.com>
# DESCRIPTION:    Apache Image Container

FROM dockerbase/service

MAINTAINER Richad Lee "lifuzu@gmail.com"

ENV LC_ALL C
ENV DEBIAN_FRONTEND noninteractive

# Run the build scripts
RUN	apt-get update

ENV     PKG_NAME apache2
# Install Apache
RUN     apt-get install -y --no-install-recommends apache2

#RUN	chown -R www-data:www-data /usr/share/apache2
RUN     mkdir -p /etc/service/$PKG_NAME
ADD     build/runit/$PKG_NAME /etc/service/$PKG_NAME/run

# Clean up system
RUN	apt-get clean
RUN	rm -rf /tmp/* /var/tmp/*
RUN	rm -rf /var/lib/apt/lists/*

# Define mountable directories.
VOLUME 	["/etc/apache2/sites-enabled", "/etc/apache2/available", "/var/www", "/var/log/apache2"]

# for main ports:
EXPOSE  80 
EXPOSE  443 

# Set environment variables.
ENV     HOME /root

# Define working directory.
WORKDIR /root

# Define default command.
CMD ["bash"]

