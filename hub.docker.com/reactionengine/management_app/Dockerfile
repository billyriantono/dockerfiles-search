FROM docker.io/ubuntu:18.10
MAINTAINER Viktor Horvath <support@reaction-engine.org>

# create folder for the reaction components
RUN mkdir /local && mkdir /local/reaction && mkdir /local/reaction/install && mkdir /local/reaction/install/management_app && mkdir /local/reaction/management_app_log

# update the repositories and install vim, wget, unzip and curl
RUN apt-get update -y && apt-get install -y vim wget unzip curl

# install sudo && change the pwd of root
RUN apt-get install -y sudo && echo root:root | chpasswd

#############################################################################
#                   1. install management app GUI
#############################################################################

# install tools for python3
RUN apt-get install -y python3-venv python3-dev python3-pip

# create virtual environment
RUN /usr/bin/python3.6 -m venv /local/reaction/venv

# install Apache2 with mod_wsgi
RUN apt-get install -y apache2 apache2-dev
RUN apt-get install build-essential && /bin/bash -c "source /local/reaction/venv/bin/activate && pip install -I mod_wsgi==4.6.4"
# Apache ENVs
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_PID_FILE /var/run/apache2/apache2.pid
ENV APACHE_SERVER_NAME localhost
ENV APACHE_RUN_DIR /var/run/apache2

# install Oracle client
RUN apt-get -y install libaio1
RUN wget https://bitbucket.org/ric_flair_wcw/reaction-storage-v1_1/downloads/oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm -P /local/reaction/install/management_app
RUN apt-get -y install alien && alien -i /local/reaction/install/management_app/oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm

# download & unzip the management app install ZIP
RUN wget https://bitbucket.org/ric_flair_wcw/reaction-storage-v1_1/downloads/reaction_management_app_v1_1.zip -P /local/reaction/install/management_app
RUN unzip /local/reaction/install/management_app/reaction_management_app_v1_1.zip -d /local/reaction/install/management_app && rm -f /local/reaction/install/management_app/reaction_management_app_v1_1.zip

# install python's dependencies
RUN apt-get install -y libssl-dev libffi-dev && apt-get install -y language-pack-en
RUN /bin/bash -c "source /local/reaction/venv/bin/activate && export LC_ALL=en_US.UTF-8 && export LC_CTYPE=en_US.UTF-8 && pip install wheel && pip install -r /local/reaction/install/management_app/requirements.txt"

# unzip the management app source ZIP
RUN unzip /local/reaction/install/management_app/management_app-1.1.zip -d /local/reaction/management_app

# setting the log location of management app
RUN sed -i "s|'filename' : 'reaction_debug.log'|'filename' : '/local/reaction/management_app_log/reaction_debug.log'|g" /local/reaction/management_app/management_app/settings_reaction.py

# configure Apache2 
RUN echo '<VirtualHost *:80>\n\
  LoadModule wsgi_module /local/reaction/venv/lib/python3.6/site-packages/mod_wsgi/server/mod_wsgi-py36.cpython-36m-x86_64-linux-gnu.so\n\
  Alias /reaction-management/static /local/reaction/management_app/static\n\
  <Directory /local/reaction/management_app/static>\n\
    Allow from all\n\
    Require all granted\n\
  </Directory>\n\
  <Directory /local/reaction/management_app/management_app>\n\
    <Files wsgi.py>\n\
      Require all granted\n\
    </Files>\n\
  </Directory>\n\
  WSGIDaemonProcess management-app python-path=/local/reaction/management_app:/local/reaction/venv/lib/python3.6/site-packages\n\
  WSGIProcessGroup management-app\n\
  WSGIScriptAlias /reaction-management /local/reaction/management_app/management_app/wsgi.py process-group=management-app\n\
  PassEnv LD_LIBRARY_PATH\n\
  PassEnv REACTION_SUBDOMAIN\n\
</VirtualHost>' > /etc/apache2/sites-available/000-default.conf
RUN echo "export REACTION_SUBDOMAIN=reaction-management" >> /etc/apache2/envvars
RUN echo "export LD_LIBRARY_PATH=/usr/lib/oracle/12.2/client64/lib" >> /etc/apache2/envvars
# adding permission to the user who runs apache2 to write to /local/reaction/management_app_log
RUN chown -R www-data:www-data /local/reaction/management_app_log

HEALTHCHECK --interval=10s --retries=10 CMD curl --fail http://localhost/reaction-management/accounts/login/

CMD ["/usr/sbin/apache2ctl", "-DFOREGROUND"]

EXPOSE 80

