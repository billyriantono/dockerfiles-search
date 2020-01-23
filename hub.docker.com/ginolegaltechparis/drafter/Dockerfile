FROM python:3.7.1

#####################################
#
# Configuration
#
#####################################

ENV VERSION_TO_INSTALL latest
ENV INSTALL_DIR /opt/drafter


#####################################
#
# Debian package installation
#
#####################################

RUN apt-get update && apt-get install -y \
  libxml2-dev\
  libxslt-dev\
  python3-dev\
  lib32z1-dev\
  gettext\
  vim-tiny\
  locales\
  nano\
  poppler-utils\
  logrotate\
  gunicorn && rm -rf /var/lib/apt/lists/*
# remove unnecessary package to reduce size
RUN apt-get autoremove -y && date +'%F %T'

ENV LANG en_US.UTF-8
RUN echo "en_US.UTF-8 UTF-8" >/etc/locale.gen
RUN locale-gen && date +'%F %T'

#####################################
#
# Mount and copy directory
#
#####################################

ADD . $INSTALL_DIR
#ADD backend-${VERSION_TO_INSTALL}.tar.gz /tmp
#RUN mv /tmp/backend-${VERSION_TO_INSTALL} $INSTALL_DIR && date +'%F %T'
# Create a data volume for logs
VOLUME /var/log/drafter
# Create a data volume for media files
VOLUME /var/www/drafter/media

VOLUME /data/drafter/sock

WORKDIR $INSTALL_DIR/drafter


#####################################
#
# Setup Drafter
#
#####################################

#RUN python $INSTALL_DIR/setup.py install && date +'%F %T'

RUN pip install -r $INSTALL_DIR/requirements.proprietary.txt && date +'%F %T'
RUN pip install -r $INSTALL_DIR/requirements.dev.txt && date +'%F %T'
# Compile languages
#RUN python /usr/local/lib/python3.4/site-packages/Django-1.7.11-py3.4.egg/django/bin/django-admin.py compilemessages && date +'%F %T'
RUN django-admin compilemessages && date +'%F %T'



#####################################
#
# Run !!!!
#
#####################################
# Create default data in db if necessary
# Run gunicorn with the right parameters
# to gather the logs
RUN touch /var/log/drafter/error.log && date +'%F %T'
WORKDIR $INSTALL_DIR/uwsgi
# logs have a date time attribute to avoid overwriting the logs in case of containe restart
#CMD gunicorn gin2.wsgi -c /etc/gunicorn.conf >> /var/log/drafter/gunicorn-`date +%d%m%y-%H%M%S`.log 2>&1
#CMD uwsgi --ini uwsgi.ini
CMD ["/bin/bash","-C","start.sh"]
