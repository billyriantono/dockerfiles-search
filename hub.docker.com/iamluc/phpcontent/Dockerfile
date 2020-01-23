FROM alpine:3.7
RUN apk --update add freeradius freeradius-mysql dos2unix mysql-client openssl bash 
LABEL Author="Sileno Brito"
LABEL Email="sobrito@i9corp.com.br"

ENV DB_FORCE_CREATE=0
ENV MYSQL_DATABASE=radius
ENV MYSQL_HOST=localhost
ENV MYSQL_USER=radius
ENV MYSQL_PASSWORD=radpass
ENV MYSQL_PORT=3306
ENV RADIUS_KEY=your_secret_key_change_it
ENV RADIUS_CLIENTS=10.0.0.0/24
ENV RAD_DEBUG=no

COPY ./init.d/radius-config /usr/bin/radius-config
COPY ./start-packages.sh /usr/bin/start-packages
COPY ./freeradius/sql.conf /etc/raddb/mods-available/sql
COPY ./freeradius/queries.conf /etc/raddb/mods-config/sql/main/mysql/queries.conf
COPY ./freeradius/default /etc/raddb/sites-available/default
COPY ./freeradius/inner-tunnel /etc/raddb/sites-available/inner-tunnel
COPY ./freeradius/clients.conf /etc/raddb/clients.conf
ADD ./freeradius/certs /etc/raddb/certs

RUN ln -sf /etc/raddb/mods-available/sql /etc/raddb/mods-enabled/sql
RUN chmod 0640 /etc/raddb/mods-available/sql \
    /etc/raddb/mods-config/sql/main/mysql/queries.conf \
    /etc/raddb/clients.conf \
    /etc/raddb/sites-available/default \
    /etc/raddb/sites-available/inner-tunnel

RUN dos2unix  /usr/bin/radius-config \
    && dos2unix /usr/bin/start-packages

RUN chmod +x  /usr/bin/radius-config \
    && chmod +x  /usr/bin/start-packages

RUN chown -R root:radius /etc/raddb

EXPOSE 1812/udp 
EXPOSE 1813/udp

WORKDIR /etc/raddb
VOLUME [ "/etc/raddb" ]
CMD [ "/usr/bin/start-packages" ]
