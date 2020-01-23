FROM ubuntu:14.04

MAINTAINER Juan M. Rube <hola@1024mbits.com> @1024mbits

# Agrego PostgreSQL PGP key para verificar Debian packages.
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys B97B0AFCAA1A47F044F244A07FCC7D46ACCC4CF8

#Actualizamos repositorio
RUN apt-get update

#Actualizamos el sistema
RUN apt-get -y upgrade

#Instalo Postgress
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ trusty-pgdg main" > /etc/apt/sources.list.d/pgdg.list && \
        apt-get update && \
        apt-get -yq install \
            adduser \
            ghostscript \
            postgresql-9.4 \
            postgresql-contrib-9.4 \
            python \
                python-pip \
                python-imaging \
                python-pychart python-libxslt1 xfonts-base xfonts-75dpi \
                libxrender1 libxext6 fontconfig \
                python-zsi \
                python-lasso \
                libzmq3 \
                gdebi

#Creamos el usuario de odoo en Postgress
RUN sudo su - postgres -c "createuser -s odoo" 2> /dev/null || true

#Instalamos openssh-server
RUN apt-get -y install openssh-server 

#Creamos el usuario de sistema odoo con la carpeta home en /opt/odoo
RUN sudo adduser --system --home=/opt/odoo --group odoo

#Instalamos las dependencias para Odoo
RUN sudo apt-get install -y python-dateutil python-decorator python-docutils python-feedparser python-gdata python-gevent python-imaging python-jinja2 python-ldap python-libxslt1 python-lxml python-mako python-mock python-openid python-passlib python-psutil python-psycopg2 python-pybabel python-pychart python-pydot python-pyparsing python-pypdf python-reportlab python-requests python-simplejson python-tz python-unittest2 python-vatnumber python-vobject python-werkzeug python-xlwt python-yaml wkhtmltopdf

#Instala git
RUN sudo apt-get -y install git

#Instalamos python-unidecode para AEAT de localizacion española
RUN sudo apt-get -y install python-unidecode

#Instalamos pyserial, pyusb, qrcode para TPV y PosBox
RUN sudo pip install pyserial
RUN sudo pip install pyusb; exit 0
RUN sudo pip install qrcode; exit 0

#Bajamos phonenumbers, py-asterisk para asterisk
RUN sudo pip install phonenumbers
RUN sudo pip install py-asterisk

#Instalamos mercurial
RUN sudo apt-get -y install mercurial

#Bajamos web_action_request, web_socketio
RUN sudo hg clone https://bitbucket.org/anybox/web_action_request
RUN sudo hg clone https://bitbucket.org/anybox/web_socketio

#Descargamos odoo de git dentro de /opt/odoo
RUN cd /opt/odoo
RUN sudo su - odoo -s /bin/bash -c "git clone https://www.github.com/odoo/odoo --depth 1 --branch 8.0 --single-branch ."

#Creamos la carpeta extras
RUN mkdir /opt/odoo/extras
RUN cd /opt/odoo/extras

#Bajamos localizacion española
RUN sudo su - odoo -s /bin/bash -c "git clone https://github.com/OCA/l10n-spain.git --depth 1 --branch 8.0 --single-branch"

#Bajamos partner-contact
RUN sudo su - odoo -s /bin/bash -c "git clone https://github.com/OCA/partner-contact.git --depth 1 --branch 8.0 --single-branch"

#Bajamos account-payment
RUN sudo su - odoo -s /bin/bash -c "git clone https://github.com/OCA/account-payment.git --depth 1 --branch 8.0 --single-branch"

#Bajamos reporting-engine
RUN sudo su - odoo -s /bin/bash -c "git clone https://github.com/OCA/reporting-engine.git --depth 1 --branch 8.0 --single-branch"

#Bajamos bank-statement-import
RUN sudo su - odoo -s /bin/bash -c "git clone https://github.com/OCA/bank-statement-import.git --depth 1 --branch 8.0 --single-branch"

#Bajamos account-financial-tools
RUN sudo su - odoo -s /bin/bash -c "git clone https://github.com/OCA/account-financial-tools.git --depth 1 --branch 8.0 --single-branch"

#Bajamos bank-payment
RUN sudo su - odoo -s /bin/bash -c "git clone https://github.com/OCA/bank-payment.git --depth 1 --branch 8.0 --single-branch"

#Bajamos connector-telephony
RUN sudo su - odoo -s /bin/bash -c "git clone https://github.com/OCA/connector-telephony.git --depth 1 --branch 8.0 --single-branch"

#Creamos fichero de configuracion /etc/odoo-server.conf  y le ponemos los permisos
# Copy entrypoint script and Odoo configuration file
COPY ./entrypoint.sh /
COPY ./odoo-server.conf /etc/odoo/
RUN chown odoo /etc/odoo/odoo-server.conf

#Copiamos el fichero de odoo-server de opensourcerer y le ponemos los permisos
ADD http://www.theopensourcerer.com/wp-content/uploads/2014/09/odoo-server /etc/init.d/odoo-server
RUN sudo chmod 755 /etc/init.d/odoo-server
RUN sudo chown root: /etc/init.d/odoo-server

#Creamos log file y permisos 
RUN sudo mkdir /var/log/odoo
RUN sudo chown odoo:root /var/log/odoo

#Actualizamos el update-rc para que se ejecute al iniciar
RUN sudo update-rc.d odoo-server defaults

#Abrimos los puertos 8069 y 8072
EXPOSE 8069 8072

# Creamos el entorno Odoo
ENV OPENERP_SERVER /etc/odoo/odoo-server.conf

#Usuario por defecto cuando corra el contenedor
USER odoo

#Hacemos ejecutable el entrypoint
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
CMD ["odoo-server"]
