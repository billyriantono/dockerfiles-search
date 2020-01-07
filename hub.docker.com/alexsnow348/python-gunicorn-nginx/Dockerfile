FROM python:3.6
MAINTAINER Alex Snow <alexsnow348@gmail.com>


# Software version management
ENV GUNICORN_VERSION=19.7.1
ENV GEVENT_VERSION=1.2.2



# Add the application resources URL
RUN echo "deb http://archive.ubuntu.com/ubuntu/ bionic main universe" >> /etc/apt/sources.list

# Update the sources list
RUN apt-get update

RUN echo "deb http://nginx.org/packages/ubuntu/ bionic nginx" >> /etc/apt/sources.list
RUN wget https://nginx.org/keys/nginx_signing.key -O - | apt-key add -
RUN apt-get update && apt-get install -y nginx supervisor --allow-unauthenticated


ENV APP_ENVIRONMENT production

# Flask demo application
COPY ./app /app
RUN pip3 install -r /app/requirements.txt

# System packages installation

# Nginx configuration
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d/nginx.conf

# Supervisor configuration
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY gunicorn.conf /etc/supervisor/conf.d/gunicorn.conf

# Gunicorn installation
RUN pip install gunicorn==$GUNICORN_VERSION gevent==$GEVENT_VERSION

# Gunicorn default configuration
COPY gunicorn.config.py /app/gunicorn.config.py

WORKDIR /app

EXPOSE 80 443

CMD ["/usr/bin/supervisord"]
