FROM ubuntu:trusty
MAINTAINER Andrew Xu <bigtaro@gmail.com>
RUN apt-get update  \
  && apt-get -y install \
  apache2 \
  libapache2-mod-wsgi \
  python-setuptools \
  python-dev \
  libxml2-dev \
  libxslt-dev \
  && apt-get clean \
  && apt-get autoclean 
RUN easy_install Flask Flask-Pypi-Proxy
RUN mkdir -p /mnt/eggs/
RUN chown www-data:www-data -R /mnt/eggs/

# Remove default VirtualHost
RUN rm -rf /etc/apache2/sites-enabled/000-default.conf
RUN rm -rf /var/www/html

COPY ./flask_pypi_proxy.wsgi  /mnt/eggs/flask_pypi_proxy.wsgi
COPY ./flask_pypi_proxy.conf  /etc/apache2/sites-enabled/flask_pypi_proxy.conf

# Set environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV APACHE_RUN_DIR /var/run/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_LOG_DIR /var/log/apache2
ENV LANG C

EXPOSE 80

CMD ["apache2", "-DFOREGROUND"]
