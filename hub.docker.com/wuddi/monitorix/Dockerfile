FROM ubuntu:18.04 
MAINTAINER Vitalii Shvets <wuddi@wuddi.in.ua>
ENV REFRESHED_AT 2019-08-20

# Set TimeZone
ENV TZ Europe/Kiev
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
# install OS packages
RUN apt-get update && apt-get upgrade -y
ADD https://www.monitorix.org/monitorix_3.11.0-izzy1_all.deb /tmp
RUN apt-get install -y rrdtool perl libwww-perl libmailtools-perl libmime-lite-perl librrds-perl libdbi-perl libxml-simple-perl libhttp-server-simple-perl libconfig-general-perl libio-socket-ssl-perl 
RUN dpkg -i /tmp/monitorix_3.11.0-izzy1_all.deb
ADD ./apcaccess /sbin/apcaccess
RUN apt-get install --no-install-recommends -y nut-client
ADD ./monitorix.conf /etc/monitorix/monitorix.conf
CMD service monitorix start && tail -F /var/log/mysql/error.log
EXPOSE 80
