# Pull base image.
FROM ubuntu:16.04

#RUN locale-gen pl_PL.UTF8
#ENV LANG pl_PL.UTF8
#ENV LC_CTYPE pl_PL.UTF-8
ARG PHANTOM_JS=phantomjs-2.1.1-linux-x86_64

RUN rm /bin/sh && ln -s /bin/bash /bin/sh


RUN \
        apt-get update && apt-get install -y gettext wget less curl build-essential software-properties-common python-software-properties vim unzip && \
        add-apt-repository ppa:openjdk-r/ppa && \
        apt-get update && \
        apt-get -y install openjdk-8-jdk && \
        update-alternatives --config java && \
        export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64/jre && \
        export JRE_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64/jre

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/jre

RUN set -x \
        && wget --progress=dot:mega https://bitbucket.org/ariya/phantomjs/downloads/$PHANTOM_JS.tar.bz2 \
        && tar xvjf $PHANTOM_JS.tar.bz2 \
        && mv $PHANTOM_JS /usr/local/share \
        && ln -sf /usr/local/share/$PHANTOM_JS/bin/phantomjs /usr/local/bin

#install TOMCAT
RUN \
        groupadd tomcat && \
        useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat && \
        cd /tmp && \
        wget --progress=dot:mega https://archive.apache.org/dist/tomcat/tomcat-8/v8.5.30/bin/apache-tomcat-8.5.30.tar.gz && \
        mkdir /opt/tomcat && \
        tar xzvf apache-tomcat-8*tar.gz -C /opt/tomcat --strip-components=1 && \
        cd /opt/tomcat && \
        chgrp -R tomcat /opt/tomcat && \
        chmod -R g+r conf && \
        chmod g+x conf && \
        chown -R tomcat /opt/tomcat

# install nodejs with puppeteer
RUN \   
		wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb && \
		dpkg -i google-chrome-stable_current_amd64.deb; apt-get -fy install && \
        curl -sL https://deb.nodesource.com/setup_10.x | bash - && \
        apt-get install -y nodejs && \
        npm install -g --allow-root --unsafe-perm=true puppeteer@1.0.0 && \
        chmod -R a+rwx /usr/lib/node_modules/puppeteer/.local-chromium && \
        cd /opt/tomcat/temp/ && \
        npm link puppeteer && \
	npm install --global yarn@1.17.3 && \
        echo "export NODE_PATH=$(npm root --quiet -g)" >> /etc/profile.d/lib.sh && \
        echo "alias node='node -e \"\`cat $1 | sed \"s/var config = {};/var config = {args: \[\'--no-sandbox\'\]};/\"\`' " >> /etc/profile.d/lib.sh

# Add admin/admin user
ADD tomcat-users.xml /opt/tomcat/conf/
ADD manager.xml /opt/tomcat/conf/Catalina/localhost/
ADD server.xml /opt/tomcat/conf/

ENV CATALINA_HOME /opt/tomcat
ENV PATH $PATH:$CATALINA_HOME/bin

EXPOSE 8080
EXPOSE 8009

#ADD tomcat.service /etc/systemd/system/
VOLUME "/opt/tomcat/webapps"
WORKDIR /opt/tomcat

#Copy webapps
COPY m3-java-capstone-1.0.war /opt/tomcat/webapps/m3-java-capstone-1.0.war



#install postgres

RUN \
        add-apt-repository "deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main" && \
        wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - && \
        apt-get update && apt-get install -y postgresql-9.6 postgresql-client-9.6 postgresql-contrib-9.6

# Run the rest of the commands as the ``postgres`` user created by the ``postgres-9.3`` package when it was ``apt-get installed``
USER postgres

# Create a PostgreSQL role named ``docker`` with ``docker`` as the password and
# then create a database `docker` owned by the ``docker`` role.
# Note: here we use ``&&\`` to run commands one after the other - the ``\``
#       allows the RUN command to span multiple lines.

RUN \
        /etc/init.d/postgresql start &&\
        psql --command "CREATE USER cloud WITH SUPERUSER PASSWORD 'cloud';" &&\
        createdb -O cloud cloud -E 'UTF8'
#       createdb -O postgres npgeek -E 'UTF8'

USER root

#ADD multitenant_init.sql /tmp/multitenant_init.sql
#RUN chmod 755 /tmp/multitenant_init.sql

#ADD init.sql /docker-entrypoint-initdb.d/init.sql
#RUN chmod 755 /docker-entrypoint-initdb.d/init.sql

ADD run.sh /bin
RUN chmod 755 /bin/run.sh

# Adjust PostgreSQL configuration so that remote connections to the database are possible.

add pg_hba.conf /etc/postgresql/9.6/main/

#RUN echo "host all  all    0.0.0.0/0  trust" >> /etc/postgresql/9.3/main/pg_hba.conf

# And add ``listen_addresses`` to ``/etc/postgresql/9.3/main/postgresql.conf``
RUN echo "listen_addresses='*'" >> /etc/postgresql/9.6/main/postgresql.conf

# Expose the PostgreSQL port
EXPOSE 5432

# Add VOLUMEs to allow backup of config, logs and databases
VOLUME  ["/etc/postgresql", "/var/log/postgresql", "/var/lib/postgresql/data"]

RUN ln -sf /usr/share/zoneinfo/Europe/Warsaw /etc/localtime

ENTRYPOINT /bin/run.sh

CMD ["bash"]
# Define default command.

#CMD ["/bin/run.sh"]

