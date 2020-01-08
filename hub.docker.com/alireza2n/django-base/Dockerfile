FROM python:3.6-stretch
MAINTAINER Alireza Amouzadeh <alireza@amouzadeh.net>

# Install packages necessary to use postgresql and django
RUN apt-get update && apt-get install -y gettext postgresql-client locales && apt-get -y clean && \
    pip --no-cache-dir install pip -U

# Create a user and group used to launch django uwsgi process
RUN groupadd django && \
    useradd -g django -m -d /opt/django -s /sbin/nologin -c "Django user" django && \
    chmod 755 /opt/django

# Set the working directory to django user home directory
WORKDIR /opt/django

# The user which should be used to execute all commands below
USER django
