# Base image
FROM ubuntu:16.04

# Add user to run the application
RUN adduser --disabled-password --gecos "" app

# Set locales
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Create application directories
RUN mkdir -p /home/app/static; \
    mkdir -p /home/app/logs; \
    mkdir -p /home/app/media; \
    mkdir -p /home/app/src; \
    mkdir -p /home/app/conf; \
    mkdir -p /home/app/scripts

# Install packages
RUN apt-get update && \
    apt-get install -y nginx supervisor vim-nox libncurses5-dev curl wget htop build-essential

# Images libs
RUN apt-get install -y libtiff5-dev libjpeg8-dev zlib1g-dev libfreetype6-dev liblcms2-dev libwebp-dev tcl8.6-dev tk8.6-dev python-tk

# Python
RUN apt-get install -y python3 python3-dev python3-pip && \
    pip3 install --upgrade pip && \
    pip3 install gunicorn

# Import conf
COPY conf /home/app/conf
COPY scripts /home/app/scripts
RUN chmod 755 -R /home/app/scripts

# Supervisord
RUN ln -s /home/app/conf/supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# NGINX
RUN echo "daemon off;" >> /etc/nginx/nginx.conf ; \
    rm /etc/nginx/sites-enabled/* ; \
    ln -s /home/app/conf/django-nginx /etc/nginx/sites-enabled/

# PostgreSQL
RUN apt-get install -y libpq-dev && \
    pip3 install psycopg2

# LXML
RUN apt-get install -y libxslt1-dev libxml2-dev lib32z1-dev zlib1g-dev python3-lxml

# Nodejs
RUN apt-get install -y git nodejs-legacy npm

# Grunt
RUN npm install -g grunt grunt-cli

# Install Django application
ONBUILD COPY . /home/app/src/
ONBUILD COPY start.sh /home/app/scripts/
ONBUILD RUN pip3 install -r /home/app/src/requirements.txt
ONBUILD RUN chown -R app:app /home/app

# RUN
EXPOSE 80
ENTRYPOINT ["/home/app/scripts/entrypoint.sh"]
