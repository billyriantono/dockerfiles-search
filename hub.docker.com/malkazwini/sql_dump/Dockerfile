FROM mysql
MAINTAINER  malkazwini@gamil.com

# Copy the sql dump schema to the /data directory
COPY sql_dump/employees.sql /data/employees.sql

# Change the working directory
WORKDIR data

CMD mysql -u $MYSQL_USER -p $MYSQL_PASSWORD $MYSQL_DATABASE_NAME < employees.sql