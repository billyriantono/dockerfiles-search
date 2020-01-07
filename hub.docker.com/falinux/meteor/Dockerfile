# DOCKER-VERSION 1.12.1
# METEOR-VERSION 1.4.1.1
FROM falinux/gulp-kor:latest

MAINTAINER William Song <ksskor@falinux.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
   apt-get install -y git curl && \
   apt-get clean && \
   rm -Rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN curl https://install.meteor.com/ |sh

EXPOSE 80

WORKDIR /work

ADD ./run_meteor.sh /run_meteor.sh

RUN chmod 755 /run_meteor.sh

CMD ["/run_meteor.sh"]
