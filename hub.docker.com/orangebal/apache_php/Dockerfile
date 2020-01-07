FROM centos:7
MAINTAINER <orangebal@naver.com>

RUN yum -y update && \
    yum -y install httpd php && \
    yum clean all
RUN echo "<?php phpinfo();" > /var/www/html/index.php

EXPOSE 80

CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
