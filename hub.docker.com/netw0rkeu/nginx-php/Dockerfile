FROM netw0rkeu/nginx:1.0.0
MAINTAINER http://github.com/netw0rkeu

RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E9C74FEEA2098A6E && echo "deb http://packages.dotdeb.org/ wheezy-php55 all" > /etc/apt/sources.list.d/php.list && apt-get update
RUN apt-get install -y supervisor php5-cli php5-curl php5-fpm php5-gd php5-mcrypt php5-mysql php5-pgsql php5-sqlite && apt-get clean
ADD etc /etc
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
CMD /usr/bin/supervisord
