FROM mysql:5.7
LABEL maintainer "Best Sira <sirawat21@gmail.com>"
ENV MYSQL_ROOT_PASSWORD="toor"
ENV MYSQL_DATABASE="db"
RUN apt-get update -y \
    && rm -rf /var/lib/apt/lists/*
RUN chmod 777 -R /var/lib/mysql
VOLUME ["/var/lib/mysql"]
EXPOSE 3306
