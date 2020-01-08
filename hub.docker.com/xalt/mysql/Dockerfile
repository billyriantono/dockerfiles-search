FROM mysql:5.6.34
MAINTAINER Philipp Göllner philipp.goellner@xaltbc.de

# Set default environment variables
ENV MYSQL_HOME          /var/lib/mysql

ENV BACKUP_HOST         false
ENV BACKUP_PATH         false
ENV BACKUP_USER         false
ENV BACKUP_KEY_FILE     /tmp/id_rsa 

# Copy the my.cnf file
COPY my.cnf /etc/mysql/conf.d
RUN chown mysql:mysql /etc/mysql/conf.d/my.cnf
RUN chmod 0640 /etc/mysql/conf.d/my.cnf

# Copy custom entrypoint
COPY configure-and-start.sh /configure-and-start.sh

# make start script executable
RUN apt-get update \
 && apt-get install -y rsync \
                       openssh-client \
 && chmod +x /configure-and-start.sh

# Overwrite entrypoint & cmd
ENTRYPOINT ["/configure-and-start.sh"]
CMD ["mysqld"]
