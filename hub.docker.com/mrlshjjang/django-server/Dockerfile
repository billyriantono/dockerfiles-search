FROM mrlshjjang/ubuntu-12.04
MAINTAINER mrlshjjang <mrlshjjang@gmail.com>
RUN (echo "deb http://archive.ubuntu.com/ubuntu/ precise main restricted universe multiverse" > /etc/apt/sources.list && echo "deb http://archive.ubuntu.com/ubuntu/ precise-updates main restricted universe multiverse" >> /etc/apt/sources.list && echo "deb http://archive.ubuntu.com/ubuntu/ precise-backports main restricted universe multiverse" >> /etc/apt/sources.list && echo "deb http://archive.ubuntu.com/ubuntu/ precise-security main restricted universe multiverse" >> /etc/apt/sources.list)
RUN apt-get update

# passwod 설정없이 넘어가기..
ENV DEBIAN_FRONTEND noninteractive

ADD . /opt/django/

# ngix config
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN rm /etc/nginx/sites-enabled/default
RUN ln -s /opt/django/django.conf /etc/nginx/sites-enabled/
RUN ln -s /opt/django/supervisord.conf /etc/supervisor/conf.d/

VOLUME ["/opt/django/app"]

EXPOSE 80 22

CMD ["/opt/django/run.sh"]
