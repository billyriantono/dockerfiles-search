FROM python:3.7-stretch
LABEL maintainer="Fitiavana Ramanandafy <fitiavana.ramanandafy@gmail.com>"

# Software versions
ENV NGINX_VERSION=1.17.2-1~stretch \
    GUNICORN_VERSION=19.9.0 \
    EVENTLET_VERSION=0.25.0 \
    FLASK_VERSION=1.1.1 \
    APP_ENVIRONMENT=production

# Install nginx and supervisor
RUN echo "deb http://nginx.org/packages/mainline/debian/ stretch nginx" >> /etc/apt/sources.list \
    && wget https://nginx.org/keys/nginx_signing.key -O - | apt-key add - \
    && apt-get update && apt-get install -y nginx=$NGINX_VERSION \
                                            supervisor \
    && rm -rf /var/lib/apt/lists/*

# Nginx config
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
COPY conf/nginx.nginx /etc/nginx/conf.d/default.conf

# Supervisor config
COPY conf/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY conf/supervisord_nginx.conf /etc/supervisor/conf.d/nginx.conf
COPY conf/supervisord_gunicorn.conf /etc/supervisor/conf.d/gunicorn.conf

# Gunicorn config
COPY conf/gunicorn.config.py /etc/gunicorn/gunicorn.config.py

# Upgrade PIP, install requirements, Gunicorn and eventlet in case the user ommitted them
RUN pip install -U pip \
    && pip install gunicorn==$GUNICORN_VERSION \
                   eventlet==$EVENTLET_VERSION \
                   Flask==$FLASK_VERSION

# Sample app
COPY . /app

# 80 for HTTP and 443 for HTTPS
EXPOSE 80

# Run all with supervisord
CMD /usr/bin/supervisord
