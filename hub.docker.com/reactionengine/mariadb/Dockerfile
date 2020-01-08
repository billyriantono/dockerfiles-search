FROM mariadb:10.4.4-bionic
MAINTAINER Viktor Horvath <support@reaction-engine.org>

ENV MYSQL_ROOT_PASSWORD=root \
    MYSQL_DATABASE=reactionstore \
    TZ='Europe/London'

# instaling wget
RUN apt-get update -y && apt-get install -y wget

# creating SQL file to create reaction DB user and do the job of mysql_secure_installation
RUN echo 'CREATE USER "reaction"@"%" IDENTIFIED BY "reactionengine";\
GRANT ALL PRIVILEGES ON reactionstore.* TO "reaction"@"%";\
DELETE FROM mysql.user WHERE User="";\
DELETE FROM mysql.user WHERE User="root" AND Host NOT IN ("localhost", "127.0.0.1", "::1");\
DROP DATABASE IF EXISTS test;\
DELETE FROM mysql.db WHERE Db="test" OR Db="test\\_%";\
FLUSH PRIVILEGES;' > /tmp/create_user.sql

# creating /etc/my.cnf
RUN echo '[mysqld]\n\
# Disabling symbolic-links is recommended to prevent assorted security risks\n\
symbolic-links = 0\n\
autocommit = 0\n\
lower_case_table_names = 1\n\
transaction-isolation = READ-COMMITTED\n\
bind-address=0.0.0.0\n\
# include all files from the config directory\n\
!includedir /etc/mysql/conf.d/' > /etc/my.cnf

# getting the scheme SQL file
RUN wget https://bitbucket.org/ric_flair_wcw/reaction-storage-v1_1/downloads/create_tables_mysql.sql  -P /tmp

# execute the SQL files at initializing
RUN echo '#!/bin/bash\n\
 mysql -h "localhost" -u "root" "-proot" "reactionstore" < "/tmp/create_tables_mysql.sql"\n\
 mysql -h "localhost" -u "root" "-proot" "reactionstore" < "/tmp/create_user.sql"\n\
 touch /tmp/healthy' > /docker-entrypoint-initdb.d/create-reaction-db.sh

HEALTHCHECK --interval=10s --retries=30 CMD cat /tmp/healthy

EXPOSE 3306
