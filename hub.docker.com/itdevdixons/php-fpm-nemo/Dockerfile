FROM itdevdixons/ubuntu:12.04

MAINTAINER Viliam Husar viliam.husar@dixonscarphonegroup.com

ENV DEBIAN_FRONTEND noninteractive

# Install php-fpm
RUN apt-get update && apt-get -y install php5-fpm php5-gd php5-mcrypt php5-memcache php5-mysql php5-xmlrpc

# Install sqlrelay libraries
ADD libraries/librudiments-0.32-3~e-merchant4.so.1.0.0 /usr/lib/librudiments-0.32-3~e-merchant4.so.1.0.0
RUN ln -fs /usr/lib/librudiments-0.32-3~e-merchant4.so.1.0.0 /usr/lib/librudiments-0.32-3~e-merchant4.so.1

ADD libraries/libsqlrclient-0.41-2~e-merchant24.so.1.0.0 /usr/lib/libsqlrclient-0.41-2~e-merchant24.so.1.0.0
RUN ln -fs /usr/lib/libsqlrclient-0.41-2~e-merchant24.so.1.0.0 /usr/lib/libsqlrclient-0.41-2~e-merchant24.so.1

ADD libraries/sql_relay.so /usr/lib/php5/20090626/sql_relay.so

ADD confd /etc/confd/
ADD php5/conf.d /etc/php5/conf.d/

ADD run.sh /usr/local/bin/run
RUN chmod +x /usr/local/bin/run

EXPOSE 9000

CMD /usr/local/bin/run