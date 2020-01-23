FROM eboraas/laravel

MAINTAINER Didi Roesmana "didileeee@gmail.com"

RUN groupadd --gid 1000 node \
  && useradd --uid 1000 --gid node --shell /bin/bash --create-home node

ADD http://httpredir.debian.org/debian/project/trace/ftp-master.debian.org /etc/trace_ftp-master.debian.org
ADD http://security.debian.org/project/trace/security-master.debian.org /etc/trace_security-master.debian.org

RUN apt-get update

RUN apt-get -y install curl python-software-properties

RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -

RUN apt-get install nodejs

EXPOSE 80
EXPOSE 443

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]  