FROM phusion/baseimage:latest

MAINTAINER Jakub Zubielik <jakub.zubielik@scalac.io>

RUN apt-get update && \
    apt-get upgrade -y -o Dpkg::Options::="--force-confold" && \
    apt-get install -y --force-yes postgresql

RUN mkdir -p /etc/my_init.d

RUN touch /tmp/init.sh

RUN echo '#!/bin/bash\n\
bash /tmp/init.sh || exit 0' \
> /etc/my_init.d/01-load-env

RUN chmod +x /etc/my_init.d/01-load-env

RUN echo '#!/bin/bash\n\
sed -i -e "s/#listen_addresses = 'localhost'/listen_addresses = '*'/" /etc/postgresql/9.3/main/postgresql.conf\n\
echo "host    all             all             0.0.0.0/0                md5" >> /etc/postgresql/9.3/main/pg_hba.conf\n\
su - postgres -c "/usr/lib/postgresql/9.3/bin/postgres -i -D /var/lib/postgresql/9.3/main -c config_file=/etc/postgresql/9.3/main/postgresql.conf &"\n\
sleep 2' \
> /etc/my_init.d/02-postgres

RUN chmod +x /etc/my_init.d/02-postgres

RUN touch /tmp/init.sql

RUN echo '#!/bin/bash\n\
su - postgres -c "psql -f /tmp/init.sql" || exit 0\n\' \
> /etc/my_init.d/03-load-data

RUN chmod +x /etc/my_init.d/03-load-data

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 5432

CMD ["/sbin/my_init"]
