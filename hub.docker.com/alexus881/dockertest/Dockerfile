FROM mysql
Label Author="akorotkov"
ENV MYSQL_ROOT_PASSWORD root
COPY createdb.sql /opt/
COPY init.sh /opt/
RUN chmod +x /opt/init.sh
WORKDIR /opt
ENTRYPOINT /opt/init.sh && /bin/sh

