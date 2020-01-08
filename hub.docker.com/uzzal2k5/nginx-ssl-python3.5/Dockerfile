FROM ubuntu:16.04

MAINTAINER uzzal < uzzal2k5@gmail.com >

# Install required packages and remove the apt packages cache when done.

RUN apt-get update && \
    apt-get install -y locales


# This is for Languaage  Generalization UTF-8
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get install -y openssl net-tools \
    libssl-dev \
    net-tools \
	nginx
	# Set the locale

RUN apt-get install -y build-essential libssl-dev libffi-dev python3-dev
RUN apt-get install -y python3-pip
RUN apt-get update && \
    apt-get install -y mysql-client libmysqlclient-dev

# install uwsgi now because it takes a little while
RUN python3 -m pip install --upgrade pip

RUN pip3 install uwsgi
RUN pip3 install gunicorn psycopg2
RUN pip3 install mysqlclient
COPY req/requirements.txt /
RUN chmod a+x /requirements.txt
RUN pip3 install -r /requirements.txt
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
	&& ln -sf /dev/stderr /var/log/nginx/error.log
RUN mkdir /etc/ssl/ssl_certs
COPY ssl/* /etc/ssl/ssl_certs/
COPY config/ssl_web_config  /etc/nginx/sites-available/
RUN ln -sf /etc/nginx/sites-available/ssl_web_config /etc/nginx/sites-enabled/ssl_web_config
RUN ln -sf /usr/bin/python3    /usr/bin/python
COPY config/.htaccess   /var/www/
RUN sed -i 's/# server_tokens off/server_tokens off/g' /etc/nginx/nginx.conf

EXPOSE 80 443

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]



