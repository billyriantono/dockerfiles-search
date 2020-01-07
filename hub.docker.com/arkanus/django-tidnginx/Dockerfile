# Centos7 with django + uWSGI + nginx

FROM arkanus/django-tidevelop
MAINTAINER Marcos Sánchez <arkanus@gmail.com>

RUN yum install -y -q \
			nginx \
			supervisor

RUN pip install uWSGI
ENV UWSGI_MODULE="example.wsgi:application"

ADD nginx.conf /etc/nginx/nginx.conf
ADD uwsgi.ini /etc/
ADD supervisord.conf /etc/supervisord.d/app.ini

CMD ["supervisord", "-n", "-c", "/etc/supervisord.conf"]
