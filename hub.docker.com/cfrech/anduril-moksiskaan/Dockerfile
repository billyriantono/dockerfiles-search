FROM cfrech/anduril-base

ADD commons-net-3.3.tar.gz /opt
ADD hibernate-release-4.3.5.Final.tar.gz /opt
ADD moksiskaan.tar.gz /opt
ADD moksiskaan-20150327.dbdump.tar.gz /opt

RUN ln -s /opt/hibernate-release-4.3.5.Final /opt/hibernate

# postgresql
RUN echo 'deb http://apt.postgresql.org/pub/repos/apt/ wheezy-pgdg main' >> /etc/apt/sources.list.d/pgdg.list
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN apt-get update && apt-get install -y postgresql-9.1

# setup database
RUN service postgresql start && su postgres -c "psql -c \"CREATE USER moksiskaan PASSWORD 'moksiskaan';\"" && service postgresql stop
RUN service postgresql start && su postgres -c "psql -c \"CREATE DATABASE moksiskaan WITH OWNER=moksiskaan encoding='UTF-8' LC_CTYPE='en_US.utf8' LC_COLLATE='en_US.utf8' TEMPLATE template0;\"" && service postgresql stop
RUN service postgresql start && su postgres -c "psql moksiskaan -f /opt/moksiskaan-20150327.dbdump" && service postgresql stop

RUN chmod a+x /opt/moksiskaan/db/piispanhiippa
ENV MOKSISKAAN_HOME /opt/moksiskaan/db
ENV HIBERNATE_DIR /opt/hibernate
ENV CLASSPATH :/opt/moksiskaan/db/etc:/opt/hibernate/lib/jpa/hibernate-entitymanager-4.3.5.Final.jar:/opt/hibernate/lib/required/hibernate-jpa-2.1-api-1.0.0.Final.jar:/opt/hibernate/lib/required/dom4j-1.6.1.jar:/opt/hibernate/lib/required/jboss-transaction-api_1.2_spec-1.0.0.Final.jar:/opt/hibernate/lib/required/jboss-logging-annotations-1.2.0.Beta1.jar:/opt/hibernate/lib/required/hibernate-core-4.3.5.Final.jar:/opt/hibernate/lib/required/javassist-3.18.1-GA.jar:/opt/hibernate/lib/required/jboss-logging-3.1.3.GA.jar:/opt/hibernate/lib/required/jandex-1.1.0.Final.jar:/opt/hibernate/lib/required/antlr-2.7.7.jar:/opt/hibernate/lib/required/hibernate-commons-annotations-4.0.4.Final.jar:/opt/hibernate/lib/optional/c3p0/hibernate-c3p0-4.3.5.Final.jar:/opt/hibernate/lib/optional/c3p0/mchange-commons-java-0.2.3.4.jar:/opt/hibernate/lib/optional/c3p0/c3p0-0.9.2.1.jar

RUN usermod -a -G postgres anduril

COPY init.sh /home/anduril/init.sh
RUN chmod 777 /home/anduril/init.sh
ENTRYPOINT ["/home/anduril/init.sh"]
