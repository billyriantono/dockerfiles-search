FROM odoo:10

USER root
RUN echo 'deb http://deb.debian.org/debian stretch-backports main' > /etc/apt/sources.list.d/backports.list
RUN apt-get update
RUN apt-get install -y -t stretch-backports libpq5 postgresql-client-9.6
RUN apt-get install -y libssl-dev build-essential python-dev python-cffi libffi-dev
RUN pip install --upgrade setuptools 
RUN pip install pysftp enum codicefiscale 
RUN pip install pyxb==1.2.5 unidecode
VOLUME /var/lib/odoo
USER odoo
