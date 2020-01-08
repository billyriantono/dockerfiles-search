FROM bvuser/centos7:1.0
#MAINTAINER The BVLab Devops Team <sype@beezzonline.com>

RUN yum -y update 
RUN yum clean all
RUN yum -y install sudo epel-release; yum clean all
RUN yum -y install postgresql-server postgresql postgresql-contrib
RUN yum clean all

ADD ./postgresql-setup /usr/bin/postgresql-setup
ADD ./start_postgres.sh /start_postgres.sh
ADD ./supervisord.conf /etc/supervisord.conf


#Sudo requires a tty. fix that.
RUN sed -i 's/.*requiretty$/#Defaults requiretty/' /etc/sudoers
RUN chmod +x /usr/bin/postgresql-setup
RUN chmod +x /start_postgres.sh
RUN mkdir /docker-entrypoint-initdb.d
RUN /usr/bin/postgresql-setup initdb

ADD ./postgresql.conf /var/lib/pgsql/data/postgresql.conf

RUN chown -v postgres.postgres /var/lib/pgsql/data/postgresql.conf

RUN echo "host    all             all             0.0.0.0/0               md5" >> /var/lib/pgsql/data/pg_hba.conf
RUN echo "host    epermits        epermits        0.0.0.0/0               md5" >> /var/lib/pgsql/data/pg_hba.conf
RUN echo "host    activiti        activiti        0.0.0.0/0               md5" >> /var/lib/pgsql/data/pg_hba.conf
RUN echo "host    lportal         liferay         0.0.0.0/0               md5" >> /var/lib/pgsql/data/pg_hba.conf
RUN echo "host    alfresco        alfresco       0.0.0.0/0               md5" >> /var/lib/pgsql/data/pg_hba.conf
RUN echo "host    all             postgres            0.0.0.0/0           trust" >> /var/lib/pgsql/data/pg_hba.conf

COPY  docker-entrypoint-initdb.d/load_dump.sh /docker-entrypoint-initdb.d/load_dump.sh
COPY  docker-entrypoint-initdb.d/dump_epermits.sql /docker-entrypoint-initdb.d/dump_epermits.sql
COPY  docker-entrypoint-initdb.d/creatuser.sql /docker-entrypoint-initdb.d/creatuser.sql
COPY  docker-entrypoint.sh docker-entrypoint.sh
COPY  createAll.sql docker-entrypoint-initdb.d
COPY  createAppUsers.sql docker-entrypoint-initdb.d
COPY  createDbComonCmd.sql docker-entrypoint-initdb.d
COPY  createDbEnvIntAm_V2.sql docker-entrypoint-initdb.d
COPY  createDbEnvIntBj.sql docker-entrypoint-initdb.d
COPY  createDbEnvIntLn.sql docker-entrypoint-initdb.d
COPY  createDbEnvRecAm_V1.sql docker-entrypoint-initdb.d
COPY  createDbEnvRecAm_V2.sql docker-entrypoint-initdb.d
COPY  createDbEnvRecBj.sql docker-entrypoint-initdb.d
COPY  createDbEnvRecLn.sql docker-entrypoint-initdb.d
COPY  createDbEnvSnbAm_V2.sql docker-entrypoint-initdb.d
COPY  createDbEnvSnbBj.sql docker-entrypoint-initdb.d
COPY  createDbEnvSnbLn.sql docker-entrypoint-initdb.d
COPY  createDbEnvTraAm_V2.sql docker-entrypoint-initdb.d
COPY  createDbEnvtraBj.sql docker-entrypoint-initdb.d
COPY  createDbEnvTraLn.sql docker-entrypoint-initdb.d
COPY  createDbEnvUatAm_V2.sql docker-entrypoint-initdb.d
COPY  createDbEnvUatBj.sql docker-entrypoint-initdb.d
COPY  createDbEnvUatLn.sql docker-entrypoint-initdb.d
RUN   chmod +x /docker-entrypoint-initdb.d/*sh

#creation user deployer 
RUN useradd -d /home/deployer -m deployer && mkdir /home/deployer/.ssh
RUN echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDLPqBcb8x/L03D0+FuJSwxXAuqmAeGzKdfNnezN24NZvP+b2s3m79kiUaN0HjDtPSNQqR9sgX8SMhNevaK/j9+qo1Zq3jSGax8czTEaZdNbcu+gfXTbek4YSnle6LR/5poELV5NA4auNfpYpnZ8mC7OwWXaisKkJ19YQDb4TUKQ7W1ThIsgKqu6/8fQd3+UZES0aprTumggvBhA6OXy3xuFqwF42lPD62q1F+PcbSGaAh6OUG2627KHipkRy0swtVVH+LTFutinxGNULt9V1uyuwBqlBBIfBH8S++8ZJAAT+zUPScLvbLJGJnmMx2QL5t3djSAhcQSekhYbkbypis3 deployer-key" > /home/deployer/.ssh/authorized_keys
RUN chown deployer: /home/deployer/.ssh/authorized_keys
RUN chmod 600 /home/deployer/.ssh/authorized_keys
RUN touch /etc/sudoers.d/90-cloud-init-users
RUN chmod 644 /etc/sudoers.d/90-cloud-init-users
RUN echo "deployer ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/90-cloud-init-users

#cl user postgres
RUN usermod -m -d /home/postgres -s /bin/bash postgres
mkdir /home/deployer/.ssh
RUN echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQCfuApGSAalHqD+OFAUzKQNFn5kwo5gSVslcai6obO1grI5iVVHbTWTfWxmC7QhTJ1hC1mWYpgLVYw93TLp2TRw0oIg/sbrQZUey0TmbHrcEmKX55ee7Cq6dr+TE2A5EXxe7BNVwkqP6P2MZ+8Xb3o5ZVBS/SB3fYOKkmwonMWCNGFtYoxHFv5L/m40CW9PIuVrv4c+swsCazpAavzTBGkAW6+/QNt26yTr9FCMEH+vZUS302bb0sV2oiPNwkW0AN0yEjhmstxuI2uNcjvZQtJ4D/rRpy4wpjh1erilCPdj1oF5eM44lfOZqwzVzQzqUw+8qb1OaGzg+dGzluxBiXwv postgres" > /home/postgres/.ssh/authorized_keys
COPY private/id_rsa /home/postgres/.ssh/id_rsa
RUN chown postgres: /home/postgres/.ssh/id_rsa
RUN chown postgres: /home/postgres/.ssh/authorized_keys
RUN chmod 600 /home/postgres/.ssh/id_rsa
RUN chmod 600 /home/postgres/.ssh/authorized_keys

ENTRYPOINT ["/docker-entrypoint.sh"]
VOLUME ["/var/lib/pgsql"]

EXPOSE 5432

CMD ["/bin/bash", "/start_postgres.sh"]
