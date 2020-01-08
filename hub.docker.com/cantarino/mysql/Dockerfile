FROM mysql

LABEL maintainer="Rodrigo Cantarino <rodrigopcantarino@gmail.com>"

# Set Timezone
ENV TZ=America/Sao_Paulo
# Set ENVIROMENT VARIABLES
ENV MYSQL_DATABASE="gacoss"
ENV MYSQL_USER="user"
ENV MYSQL_PASSWORD="user12345"
ENV MYSQL_ROOT_PASSWORD="root"
#ENV MYSQL_ROOT_HOST=%

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN chown -R mysql:root /var/lib/mysql/

# Add the content of the sql-scripts/ directory to your image
# All scripts in docker-entrypoint-initdb.d/ are automatically
# executed during container startup
# COPY ./sql_scripts_to_execute_on_load/ /docker-entrypoint-initdb.d/

#ADD my.cnf /etc/mysql/conf.d/my.cnf

CMD ["mysqld"]


EXPOSE 3306 33060