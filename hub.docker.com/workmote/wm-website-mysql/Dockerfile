FROM workmote/base:latest

# Version number for WorkMote's Docker Website Image used for mysql.
LABEL com.workmote.they.wm.website-mysql.version="0.1"
# Maintainer for WorkMote's Docker Website Image used for mysql.
LABEL com.workmote.they.wm.website-mysql.maintainer="Daniel Dalgo <dalguete@gmail.com>"
# Purpose of anything here installed for WorkMote's Docker Website Image used for mysql.
LABEL com.workmote.they.wm.website-mysql.purpose="db"
# Application name here installed for WorkMote's Docker Website Image used for mysql.
LABEL com.workmote.they.wm.website-mysql.app="mysql"

# To avoid having errors like "unable to initialize frontend: Dialog" when packages
# are upgraded/installed.
ARG DEBIAN_FRONTEND=noninteractive

# Start everything as the expected (generally) root user, so there won't be
# installation problems in case base image has set USER to something different.
USER root

# 00
# Load debconf selections for packages to be installed.
COPY 00-packages-defaults/ /tmp/00-packages-defaults/
RUN /tmp/00-packages-defaults/packages-defaults.sh \
	&& rm -r /tmp/00-packages-defaults/

# 01
# Packages installation.
COPY 01-packages-installation/ /tmp/01-packages-installation/
RUN /tmp/01-packages-installation/packages-installation.sh \
  && rm -r /tmp/01-packages-installation/
EXPOSE 3306

# 02
# DB Server Tune Ups.
COPY 02-db-server-tuneups/ /tmp/02-db-server-tuneups/
RUN /tmp/02-db-server-tuneups/db-server-tuneups.sh \
  && rm -r /tmp/02-db-server-tuneups/

# 03
# Install phpMyAdmin.
COPY 03-phpmyadmin/ /tmp/03-phpmyadmin/
RUN /tmp/03-phpmyadmin/phpmyadmin.sh \
  && rm -r /tmp/03-phpmyadmin/
EXPOSE 80 443

# 04
# Kick off scripts scripts.
COPY 04-kick-off/kick-off /usr/local/bin/
COPY 04-kick-off/my-bindfs-mounts /etc/default/

# 05
# Set the main processes for supervisor to run. The reason of containers using this image.
COPY 05-supervisor/ /etc/supervisor/conf.d/

# 06
# Perform some final processes.
COPY 06-finally/ /tmp/06-finally/
RUN /tmp/06-finally/finally.sh \
  && rm -r /tmp/06-finally/

# 07
# Setup the user to use to trigger any process inside this contained.
ARG CUSTOM_USER_NAME="workmote"
USER ${CUSTOM_USER_NAME}