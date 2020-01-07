FROM ubuntu:14.04
MAINTAINER Rafael Acorsi <rafaelacorsi@gmail.com>

RUN locale-gen en_US.UTF-8
RUN update-locale LANG=en_US.UTF-8

RUN apt-get -qq update && \
    apt-get -y install nginx-full && \
    apt-get -y install build-essential python-dev libxml2-dev python-pip unzip wget supervisor && \
    apt-get install -y -q postgresql-9.3 \
    postgresql-contrib-9.3 postgresql-9.3-postgis-2.1 \
    libpq-dev sudo && \
    pip install --upgrade pip

RUN mkdir -p /var/log/nginx/app
RUN mkdir -p /var/log/uwsgi/app/
#RUN echo "daemon off;" >> /etc/nginx/nginx.conf

COPY gzip_static.conf /etc/nginx/conf.d/flask/gzip_static.conf
COPY gzip.conf /etc/nginx/conf.d/flask/gzip.conf
COPY uwsgi-emperor.conf /etc/init/uwsgi-emperor.conf
COPY flask.conf /etc/nginx/sites-available/flask

# setup nginx
RUN ln -s /etc/nginx/sites-available/flask /etc/nginx/sites-enabled/flask && \
    rm /etc/nginx/sites-enabled/default

RUN mkdir -p /var/log/supervisor
COPY supervisor.conf /etc/supervisor/conf.d/

copy app /var/www/app
RUN pip install -r /var/www/app/requirements.txt

RUN mkdir /etc/ssl/private-copy
RUN mv /etc/ssl/private/* /etc/ssl/private-copy/
RUN rm -r /etc/ssl/private
RUN mv /etc/ssl/private-copy /etc/ssl/private
RUN chmod -R 0700 /etc/ssl/private
RUN chown -R postgres /etc/ssl/private

ADD postgresql.conf /etc/postgresql/9.3/main/postgresql.conf
ADD pg_hba.conf /etc/postgresql/9.3/main/pg_hba.conf
RUN chown postgres:postgres /etc/postgresql/9.3/main/*.conf
ADD run /usr/local/bin/run
RUN chmod +x /usr/local/bin/run

COPY uwsgi.ini /var/www/uwsgi.ini

EXPOSE 5000 7000
CMD ["supervisord", "-n"]
