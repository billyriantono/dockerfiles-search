FROM centurylink/drupal:latest
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install mcrypt php5-mcrypt
RUN php5enmod mcrypt
VOLUME ["/etc/apache2/", "/var/log/apache2/", "/app/"]
