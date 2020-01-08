FROM centos:7
MAINTAINER miko@cafelounge.net

# component 
RUN cd /tmp \
 && yum reinstall -y glibc-common \
 && yum -y install epel-release iproute iputils iptables nc \
 && yum clean all \
 && rm -rf /var/tmp/* /var/lib/yum/* /var/cache/yum/* \
 && curl -o /usr/bin/gosu -SL "https://github.com/tianon/gosu/releases/download/1.9/gosu-amd64" \
 && chmod +x /usr/bin/gosu \
 && localedef --delete-from-archive $(localedef --list-archive | grep -v -i -e "^en" -e "^ja" | xargs ) \
 && mv /usr/lib/locale/locale-archive.tmpl /usr/lib/locale/locale-archive.dist \
 && mv /usr/lib/locale/locale-archive /usr/lib/locale/locale-archive.tmpl \
 && /usr/sbin/build-locale-archive \
 && mv -f /usr/lib/locale/locale-archive.dist /usr/lib/locale/locale-archive.tmpl \
 && ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime \
 && rm -f /sbin/sln \
 && rm -rf /etc/ld.so.cache \
 && rm -rf /var/cache/ldconfig/*

# shell
ENV HOME=/root LANG=ja_JP.UTF-8
WORKDIR /root

# entry
COPY init prepare /boot/
ENTRYPOINT ["/boot/init"]
