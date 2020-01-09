FROM kdihalas/base
MAINTAINER Kostas Dihalas <kdihalas@dwhite.gr>

RUN apt-get install -y beanstalkd

EXPOSE 11300

CMD ["beanstalkd","-p","11300"]