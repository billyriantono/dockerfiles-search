FROM ubuntu:18.04
 
ENV DEBIAN_FRONTEND noninteractive
 
# Install and 'hold' opencpu-server so that the docker image can be tagged
RUN \
apt-get update && \
apt-get install -y software-properties-common && \
add-apt-repository -y ppa:opencpu/opencpu-2.1 && \
apt-get update && \
apt-get install -y opencpu-server && \
apt-mark hold opencpu-server
 
# Set opencpu password so that we can login
RUN \
echo "opencpu:opencpu" | chpasswd
 
RUN groupadd -g 5000 test && \
   useradd -d "/home/test" -u 5000 -g 5000 -m -s /bin/bash  test
 
# Remove default apache configs, make Port.conf empty
RUN rm -f /etc/apache2/sites-enabled/000-default.conf \
          /etc/apache2/sites-enabled/default-ssl.conf \
          /etc/ssl/private/ssl-cert-snakeoil.key && \
          > /etc/apache2/ports.conf 
 
## modify envvars
RUN /bin/sed -i 's/export APACHE_PID_FILE=.*/export APACHE_PID_FILE=\/home\/test\/apache2\/apache2$SUFFIX\/apache2.pid/g' /etc/apache2/envvars && \
   /bin/sed -i 's/export APACHE_RUN_DIR=.*/export APACHE_RUN_DIR=\/home\/test\/apache2\/run\/apache2$SUFFIX/g' /etc/apache2/envvars && \
   /bin/sed -i 's/export APACHE_LOG_DIR=.*/export APACHE_LOG_DIR=\/home\/test\/apache2\/log\/apache2$SUFFIX/g' /etc/apache2/envvars
 
## modify log file path in opencpu.conf
RUN /bin/sed -i 's/ErrorLog .*/ErrorLog \/home\/test\/opencpu\/apache_error.log/g' /etc/apache2/sites-enabled/opencpu.conf && \
   /bin/sed -i 's/CustomLog .*/ CustomLog \/home\/test\/opencpu\/apache_access.log combined/g' /etc/apache2/sites-enabled/opencpu.conf
 
# Create a copy of our code into the container.
WORKDIR /usr/local/src
COPY . /usr/local/src/app
 
# Move OpenCPU configuration files into place.
# COPY docker/configuration/opencpu_config/* /etc/opencpu/
 
# Run Potentially custom install scripts to install any dependencies
RUN /usr/bin/R --vanilla -f app/docker/installer.R
 
# Install our code as an R package on the server
# This is necessary and may change based on the files or
# application required for the installation.
 
#######################################################################
 
# RUN tar czf /tmp/fbplatforming.model.tar.gz app/ && \
#    /usr/bin/R CMD INSTALL /tmp/fbplatforming.model.tar.gz && \
 RUN  chgrp -Rf root /tmp && \
   chmod -Rf g+w  /tmp && \
   chown -R test /tmp

## Create all the required directories under user home directory
RUN mkdir -p /home/test/apache2 && \
    mkdir -p /home/test/apache2/run &&  \
    mkdir -p /home/test/apache2/run/apache2 && \
    mkdir -p /home/test/apache2/log/apache2 && \
    mkdir -p /home/test/apache2/apache2/ && \
    mkdir -p /home/test/opencpu && \
    chown -R test /home/test/apache2 && \
    chown -R test /home/test/opencpu && \
    chgrp -Rf root /home/test && \
    chmod -Rf g+w /home/test 

# Prints apache logs to stdout
RUN \
ln -sf /proc/self/fd/1 /home/test/apache2/log/apache2/access.log && \
ln -sf /proc/self/fd/1 /home/test/apache2/log/apache2/error.log && \
ln -sf /proc/self/fd/1 /home/test/opencpu/apache_access.log && \
ln -sf /proc/self/fd/1 /home/test/opencpu/apache_error.log


EXPOSE 8004

# switch User
USER test

## Have a entry point to start apache
ENTRYPOINT [ "/usr/sbin/apachectl", "-D", "FOREGROUND" ]
