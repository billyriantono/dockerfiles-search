FROM openjdk:8u181-jre
MAINTAINER Orlando L Otero <orlando.otero@asimio.net>, https://bitbucket.org:asimio/schemaspy.git

# Manually build using command:
# docker build -t asimio/schemaspy:latest .

# Example:
# docker run -e DB_TYPE=pgsql -e DB_HOST=`hostname` -e DB_PORT=5432 -e DB_NAME=db_dvdrental -e DB_USER=user_dvdrental -e DB_PASSWD=changeit -e DB_SCHEMAS=public -v ~/Downloads/er_model-db_dvdrental:/opt/asimio/output asimio/schemaspy:latest

VOLUME /tmp

RUN \
  bash -c 'mkdir -p /opt/asimio/{lib,output}' && \
  apt-get -qq update && \
  apt-get -y upgrade && apt-get -y autoclean && apt-get -y autoremove && \
  bash -c 'DEBIAN_FRONTEND=noninteractive apt-get install -qq -y graphviz' && \
  wget --output-document=/opt/asimio/schemaSpy.jar https://github.com/schemaspy/schemaspy/releases/download/v6.0.0/schemaspy-6.0.0.jar && \
  wget -P /opt/asimio/lib http://central.maven.org/maven2/org/postgresql/postgresql/42.2.5/postgresql-42.2.5.jar && \
  rm -rf /var/lib/apt/lists/*

CMD \
  java -jar /opt/asimio/schemaSpy.jar -t $DB_TYPE -host $DB_HOST -port $DB_PORT -db $DB_NAME -u $DB_USER -p $DB_PASSWD -schemas $DB_SCHEMAS -dp /opt/asimio/lib/postgresql-42.2.5.jar -o /opt/asimio/output