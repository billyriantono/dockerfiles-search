FROM ubuntu:14.04
MAINTAINER Myung ju Kim <ming3772@gmail.com>

# Set the locale
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get update
RUN apt-get install -y build-essential git
RUN apt-get install -y python python-dev python3 python3-dev python3-pip
RUN apt-get install -y nginx supervisor mysql-server libmysqlclient-dev

RUN pip3 install glances

RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf
RUN chown -R www-data:www-data /var/lib/nginx

# UWSGI
ENV UWSGIVERSION 2.0.11.2

RUN apt-get update && apt-get install -y --no-install-recommends \
            build-essential \
            libjansson-dev \
            libpcre3-dev \
            libssl-dev \
            libxml2-dev \
            wget \
            zlib1g-dev

RUN cd /usr/src && \
    wget --quiet -O - http://projects.unbit.it/downloads/uwsgi-${UWSGIVERSION}.tar.gz | \
    tar zxvf -

RUN cd /usr/src/uwsgi-${UWSGIVERSION} && make
RUN cp /usr/src/uwsgi-${UWSGIVERSION}/uwsgi /usr/local/bin/uwsgi
RUN PYTHON=/usr/local/python3.4/bin/python3.4
RUN cd /usr/src/uwsgi-${UWSGIVERSION} && ./uwsgi --build-plugin "plugins/python python34"
RUN mkdir -p /usr/local/lib/uwsgi/plugins
RUN cp /usr/src/uwsgi-${UWSGIVERSION}/*.so /usr/local/lib/uwsgi/plugins
RUN pip3 install uwsgi

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update
RUN echo "mysql-server mysql-server/root_password password" | debconf-set-selections
RUN echo "mysql-server mysql-server/root_password_again password" | debconf-set-selections
RUN apt-get install -y mysql-server

WORKDIR /etc/mysql
RUN sed -i "s/127.0.0.1/0.0.0.0/g" my.cnf

ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
EXPOSE 3306

CMD ["/bin/bash","/entrypoint.sh"]

# Memcached
RUN apt-get install -y libmemcached-dev

# Project
ENV PROJECT_DIR /home/ubuntu/workspace/quescheetah
ADD . ${PROJECT_DIR}
RUN chown -R www-data:www-data ${PROJECT_DIR}
RUN cd ${PROJECT_DIR} && pip3 install -r requirements.txt
RUN cd ${PROJECT_DIR}/www && python3 manage.py migrate --noinput
RUN cd ${PROJECT_DIR}/www && python3 manage.py collectstatic --noinput

RUN mkdir -p /var/uwsgi/sites-available
RUN ln -s ${PROJECT_DIR}/conf/nginx-app.conf /etc/nginx/sites-enabled/
RUN ln -s ${PROJECT_DIR}/conf/uwsgi.ini /var/uwsgi/sites-available/
RUN ln -s ${PROJECT_DIR}/conf/supervisor-app.conf /etc/supervisor/conf.d/

VOLUME ["/data", "/var/log", \
		"/etc/nginx/site-enabled", "/var/log/nginx", \
		"/etc/uwsgi/apps-enabled", "/var/log/uwsgi", \
		"/var/log/supervisor", "/var/lib/mysql"]

EXPOSE 80
EXPOSE 443

CMD ["supervisord", "-n"]