FROM misryan/docker-capr
MAINTAINER Ryan <ryan@achih.tw>

RUN yum -y update ;\
    yum clean all

ADD https://bitbucket.org/misryan/imagehelper/get/master.tar.gz /
RUN tar -zxvf master.tar.gz -C /tmp/;\
    /bin/mv /tmp/misryan-imagehelper* /tmp/misryan-imagehelper;\
    /bin/mv /tmp/misryan-imagehelper/* /var/www/html;\
    /bin/rm -rf /tmp/misryan-imagehelper;\
    rm -rf /master.tar.gz

EXPOSE 80 6379

CMD ["/usr/bin/supervisord", "--configuration=/etc/supervisord.conf"]