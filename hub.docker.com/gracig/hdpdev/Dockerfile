FROM centos:7
MAINTAINER github.com/gracig

RUN yum install epel-release -y && yum clean all
RUN yum update -y && yum clean all

#Setting up systemd
ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]
ENTRYPOINT ["/usr/sbin/init"]

RUN yum install -y systemd* && yum clean all

RUN yum install -y yum-utils yum-plugin-ovl tar git curl bind-utils unzip wget && yum clean all

# Setup sshd
RUN yum install -y openssh-server openssh-clients && yum clean all
RUN systemctl enable sshd

# kerberos client
RUN yum install -y krb5-workstation && yum clean all

# initscripts (service wrapper for servicectl) is need othewise the Ambari is unable to start postgresql
RUN yum install -y initscripts && yum clean all

# Install the jq utility
RUN curl -o /usr/bin/jq http://stedolan.github.io/jq/download/linux64/jq && chmod +x /usr/bin/jq

ENV HOSTNAME horton.single.node

#Workaround to fix hostname
RUN mv /usr/bin/hostname{,.bkp}; \
  echo "echo $HOSTNAME" > /usr/bin/hostname; \
  chmod +x /usr/bin/hostname

#Install Ambari Agent
RUN echo $(grep $(hostname.bkp) /etc/hosts | cut -f1) $HOSTNAME >> /etc/hosts \
&&  wget -nv http://public-repo-1.hortonworks.com/ambari/centos6/2.x/updates/2.5.2.0/ambari.repo -O /etc/yum.repos.d/ambari.repo \
&&  wget -nv http://public-repo-1.hortonworks.com/HDP/centos6/2.x/updates/2.6.2.14/hdp.repo -O /etc/yum.repos.d/hdp.repo \
&&  yum update -y \
&&  yum install -y ambari-agent \
&&  sed -i "s/hostname=localhost/hostname=$HOSTNAME/g" /etc/ambari-agent/conf/ambari-agent.ini \
&&  echo "#!/bin/sh" >  /var/lib/ambari-agent/public_hostname.sh \
&&  echo 'echo `hostname -f`' >> /var/lib/ambari-agent/public_hostname.sh \
&&  chmod 755 /var/lib/ambari-agent/public_hostname.sh \
&&  /var/lib/ambari-agent/public_hostname.sh \
&&  sed -i '/\[agent\]/ a public_hostname_script=/var/lib/ambari-agent/public_hostname.sh' /etc/ambari-agent/conf/ambari-agent.ini \
&&  sed -i '/\[agent\]/ a hostname_script=/var/lib/ambari-agent/public_hostname.sh' /etc/ambari-agent/conf/ambari-agent.ini \
&&  yum clean all

#Install Ambari Server
RUN yum install -y ambari-server && yum clean all

#Install missing tools..
RUN yum install -y postgresql-jdbc* net-tools vim htop && yum clean all

# Define variables inside this scripts
ENV AMBARIUSER ambari
ENV AMBARIPASSWORD ambari
ENV AMBARIDATABASE ambari_db
ENV AMBARISCHEMA ambari
ENV HIVEUSER hive
ENV HIVEDATABASE hive_db
ENV HIVEPASSWORD hive
ENV SYSTEMD_IGNORE_CHROOT 1
ENV PGDATA /var/lib/pgsql/data

#Configure postgresql and write ambari and hive database schemas into it
RUN su postgres -c initdb \
&&  sed -i "s/#listen_addresses.*/listen_addresses = '*'/g" /var/lib/pgsql/data/postgresql.conf \
&&  sed -i 's/#port = 5432.*/port = 5432/g' /var/lib/pgsql/data/postgresql.conf \
&&  sed -i 's|host.*all.*all.*127.0.0.1/32.*|host all all 0.0.0.0/0 trust|g' /var/lib/pgsql/data/pg_hba.conf \
&&  sed -i 's|local.*all.*all.*|local all all trust|g' /var/lib/pgsql/data/pg_hba.conf \
&&  su postgres -c 'pg_ctl start ' \
&&  sleep 5 \
&&  echo  $" CREATE DATABASE $AMBARIDATABASE;  \
             CREATE USER $AMBARIUSER WITH PASSWORD '$AMBARIPASSWORD';  \
             GRANT ALL PRIVILEGES ON DATABASE $AMBARIDATABASE TO $AMBARIUSER; \
          " | psql -U postgres \
&&  echo $" CREATE SCHEMA $AMBARISCHEMA AUTHORIZATION $AMBARIUSER;  \
            ALTER SCHEMA $AMBARISCHEMA OWNER TO $AMBARIUSER;  \
            ALTER ROLE $AMBARIUSER SET search_path to '$AMBARISCHEMA', 'public'; \
          " | psql -U postgres -d  $AMBARIDATABASE \
&&  psql -U $AMBARIUSER -d $AMBARIDATABASE -c '\i /var/lib/ambari-server/resources/Ambari-DDL-Postgres-CREATE.sql;' \
&&  echo $" CREATE DATABASE $HIVEDATABASE; \
            CREATE USER $HIVEUSER WITH PASSWORD '$HIVEPASSWORD'; \
            GRANT ALL PRIVILEGES ON DATABASE $HIVEDATABASE TO $HIVEUSER; \
          " | psql -U postgres \
&&  su postgres -c 'pg_ctl stop' \
&&  /bin/true

# Configure ambari
RUN echo $(grep $(hostname.bkp) /etc/hosts | cut -f1) $HOSTNAME >> /etc/hosts \
&&  /usr/bin/ssh-keygen -A \
&&  /usr/sbin/sshd  \
&&  su postgres -c 'pg_ctl start ' \
&&  sleep 5 \
&&  cat /dev/zero | ssh-keygen -q -N ""  \
&&  cat  ~/.ssh/id_rsa.pub > ~/.ssh/authorized_keys  \
&&  ssh -oStrictHostKeyChecking=no root@localhost ls \
&&  ssh -oStrictHostKeyChecking=no root@$HOSTNAME ls \
&&  ambari-server setup -s --database=postgres --databasehost=$HOSTNAME \
      --databaseport=5432 --databasename=$AMBARIDATABASE \
      --postgresschema=$AMBARISCHEMA  --databaseusername=$AMBARIUSER \
      --databasepassword=$AMBARIPASSWORD \
&&  echo server.startup.web.timeout=180 >> /etc/ambari-server/conf/ambari.properties \
&&  ambari-server setup --jdbc-db=postgres --jdbc-driver=/usr/share/java/postgresql-jdbc.jar \
&&  su postgres -c 'pg_ctl stop' \
&&  /bin/true

# Install ambari components
COPY version_definitions.json /root/version_definitions.json
COPY cluster_configuration.json /root/cluster_configuration.json
COPY host_mappings.json /root/host_mappings.json

RUN echo $(grep $(hostname.bkp) /etc/hosts | cut -f1) $HOSTNAME >> /etc/hosts \
&&  /usr/sbin/sshd  \
&&  ambari-agent start \
&&  su postgres -c 'pg_ctl start ' \
&&  ambari-server start \
&&  sleep 30 \
&&  curl -H "X-Requested-By: ambari" -X POST -u admin:admin http://$HOSTNAME:8080/api/v1/version_definitions  -d @/root/version_definitions.json \
&&  curl -H "X-Requested-By: ambari" -X POST -u admin:admin http://$HOSTNAME:8080/api/v1/blueprints/singlenode -d @/root/cluster_configuration.json \
&&  curl -H "X-Requested-By: ambari" -X POST -u admin:admin http://$HOSTNAME:8080/api/v1/clusters/singlenode -d @/root/host_mappings.json \
&&  date \
&&  time sh -c 'tail -n +0 --pid=$$ -F /var/log/ambari-server/ambari-audit.log | { sed "/.*Install.*host.*COMPLETED.*\|.*Install.*host.*FAILED.*/ q" && kill $$ ;}' || /bin/true \
&&  grep '.*Install.*host.*COMPLETED.*' /var/log/ambari-server/ambari-audit.log \
&&  ambari-server stop \
&&  ambari-agent stop \
&&  su postgres -c 'pg_ctl stop' \
&&  /bin/true


RUN mv /usr/bin/hostname{.bkp,} \
&&  systemctl enable postgresql \
&&  systemctl enable ambari-agent \
&&  systemctl enable ambari-server

