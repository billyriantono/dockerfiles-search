FROM ubuntu:xenial
RUN apt-get -y -q update
RUN apt-get -y -q upgrade

ADD resources /resources
WORKDIR /resources

RUN apt-get -y install python3 python3-pip

RUN apt-get install -y build-essential
RUN apt-get install -y libpython3.5
RUN apt-get install -y libstdc++6
RUN apt-get install -y libxerces-c3.1
RUN apt-get install -y apache2
RUN apt-get install -y libapache2-mod-wsgi-py3
RUN apt-get install -y python3-psycopg2

RUN apt-get -y -q full-upgrade

RUN pip3 install -r requirements.txt

RUN dpkg -i frepple_*.deb
RUN apt-get -f -y -q install

RUN a2enmod expires
RUN a2enmod wsgi
RUN a2enmod ssl
RUN a2ensite default-ssl
RUN a2ensite frepple
RUN service apache2 restart

EXPOSE 8000

COPY resources/entrypoint.sh /
RUN ["chmod", "+x", "/entrypoint.sh"]

ENTRYPOINT ["/entrypoint.sh"]
CMD service apache2 restart


# RUN apt-get install -y software-properties-common wget
# RUN add-apt-repository "deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main"
# RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
# RUN apt-get update
# RUN apt-get -y install postgresql-9.6
# RUN su - postgres

# RUN psql template1 -c "create user frepple with password 'frepple'"
# RUN psql template1 -c "create database frepple encoding 'utf-8' owner frepple"
# RUN psql template1 -c "create database scenario1 encoding 'utf-8' owner frepple"
# RUN psql template1 -c "create database scenario2 encoding 'utf-8' owner frepple"
# RUN psql template1 -c "create database scenario3 encoding 'utf-8' owner frepple"
# RUN exit

# RUN sed -i 's/local\(\s*\)all\(\s*\)all\(\s*\)peer/local\1all\2all\3\md5/g' /etc/postgresql/9.*/main/pg_hba.conf
# RUN service postgresql restart