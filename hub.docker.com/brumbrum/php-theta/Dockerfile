FROM brumbrum/php
MAINTAINER Alessandro Lattao <alessandro.lattao@brumbrum.it>

RUN \
  apt-get update && \
  apt-get -y --no-install-recommends install iw rfkill iproute2 wpasupplicant isc-dhcp-client net-tools iputils-ping && \
  apt-get -y autoclean && \
  apt-get -y clean && \
  apt-get -y autoremove

# configure php-fpm
RUN rm /etc/php/7.0/fpm/pool.d/www.conf
ADD pool.d/www.conf /etc/php/7.0/fpm/pool.d/www.conf

# riconfiguro l'entrypoint
RUN rm /entrypoint.sh
ADD bin/entrypoint.sh /entrypoint.sh
RUN ["chmod", "+x", "/entrypoint.sh"]
ENTRYPOINT ["/entrypoint.sh"]
