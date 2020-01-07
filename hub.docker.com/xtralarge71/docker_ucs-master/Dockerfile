FROM univention/ucs-master-amd64:latest
RUN univention-install -y locales
RUN univention-install -y acl

RUN  echo "@reboot root /usr/sbin/ucr set interfaces/eth0/netmask=\"\$(/sbin/ifconfig eth0 | awk '/netmask/{print \$4}')\"">/etc/cron.d/netmask
#ucr set interfaces/eth0/netmask="$(/sbin/ifconfig eth0 | awk '/netmask/{print $4}')"
