FROM workmote/base:latest

# Version number for WorkMote's Docker Website Image used for apache2.
LABEL com.workmote.they.wm.website-apache2.version="0.1"
# Maintainer for WorkMote's Docker Website Image used for apache2.
LABEL com.workmote.they.wm.website-apache2.maintainer="Daniel Dalgo <dalguete@gmail.com>"
# Purpose of anything here installed for WorkMote's Docker Website Image used for apache2.
LABEL com.workmote.they.wm.website-apache2.purpose="web"
# Application name here installed for WorkMote's Docker Website Image used for apache2.
LABEL com.workmote.they.wm.website-apache2.app="apache2"

# To avoid having errors like "unable to initialize frontend: Dialog" when packages
# are upgraded/installed.
ARG DEBIAN_FRONTEND=noninteractive

# Start everything as the expected (generally) root user, so there won't be
# installation problems in case base image has set USER to something different.
USER root

# 00
# Packages installation.
COPY 00-packages-installation/ /tmp/00-packages-installation/
RUN /tmp/00-packages-installation/packages-installation.sh \
  && rm -r /tmp/00-packages-installation/
EXPOSE 80 443

# 01
# Web Server Tune Ups.
COPY 01-web-server-tuneups/ /tmp/01-web-server-tuneups/
RUN /tmp/01-web-server-tuneups/web-server-tuneups.sh \
  && rm -r /tmp/01-web-server-tuneups/

# 02
# Enable SSL.
COPY 02-enable-ssl/ /tmp/02-enable-ssl/
RUN /tmp/02-enable-ssl/enable-ssl.sh \
  && rm -r /tmp/02-enable-ssl/

# 03
# Install Composer.
COPY 03-composer/ /tmp/03-composer/
RUN /tmp/03-composer/composer.sh \
  && rm -r /tmp/03-composer/

# 04
# Install Drush.
COPY 04-drush/ /tmp/04-drush/
RUN /tmp/04-drush/drush.sh \
  && rm -r /tmp/04-drush/

# 05
# Kick off scripts scripts.
COPY 05-kick-off/kick-off /usr/local/bin/
COPY 05-kick-off/my-bindfs-mounts /etc/default/

# 06
# Set the main processes for supervisor to run. The reason of containers using this image.
COPY 06-supervisor/ /etc/supervisor/conf.d/

# 07
# Perform some final processes.
COPY 07-finally/ /tmp/07-finally/
RUN /tmp/07-finally/finally.sh \
  && rm -r /tmp/07-finally/

# 11
# Setup the user to use to trigger any process inside this contained.
ARG CUSTOM_USER_NAME="workmote"
USER ${CUSTOM_USER_NAME}