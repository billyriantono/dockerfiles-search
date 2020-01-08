FROM mysql/mysql-server:latest

MAINTAINER Svetli Nikolov

# Copy config files
COPY my.cnf /etc/my.cnf
RUN chmod 0640 /etc/my.cnf

# Show mysql version
RUN mysql --version
