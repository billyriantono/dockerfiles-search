FROM chedi/f20_micro
MAINTAINER Chedi Toueiti <chedi.toueiti@gmail.com>

RUN yum install nginx openssh-server supervisor -y && \
                                                      \
    yum clean all && yum history new               && \
    truncate -c -s 0 /var/log/yum.log              && \
    rm -fr /usr/share/docs                         && \
    mv /usr/share/locale/en_US /tmp                && \
    rm -fr /usr/share/locale/*                     && \
    mv /tmp/en_US /usr/share/locale/               && \
    rm -fr /var/lib/yum/yumdb                      && \
    rm -fr var/lib/rpm/Packages/*                  && \
    /usr/sbin/sshd-keygen                          && \
    echo 'root:chikaka' |chpasswd                  && \
    echo "daemon off;" >> /etc/nginx/nginx.conf

ADD supervisord.conf /etc/supervisord.conf

EXPOSE 22 80 443

CMD ["/bin/supervisord"]