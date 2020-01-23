FROM ubuntu:latest
LABEL maintainer="Joe Scharnitzke <jscharnitzke@hospicesource.net>"

ENV DEBIAN_FRONTEND="noninteractive"

RUN apt-get update && apt-get install -y --no-install-recommends software-properties-common
RUN apt-get update && apt-get install -y --no-install-recommends gnupg2
RUN apt-get update && apt-get install -y --no-install-recommends apt-utils
RUN apt-get update && apt-get install -y apache2
RUN add-apt-repository ppa:ondrej/php -y
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4F4EA0AAE5267A6C
RUN apt-get update && apt-get install -y php5.6 php5.6-zip php5.6-xml php5.6-mysqli

RUN a2enmod rewrite
RUN a2enmod php5.6
RUN useradd hospices
ADD apache2.conf /etc/apache2/apache2.conf
ADD bootstrap.sh /bootstrap.sh
ADD envvars /etc/apache2/envvars
ADD php.ini /etc/php/5.6/apache2/php.ini
RUN chmod 755 /bootstrap.sh

EXPOSE 80
CMD ["/bootstrap.sh"]