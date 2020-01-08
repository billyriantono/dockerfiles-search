FROM mroca/symfony-test

RUN apt-get update \
    && apt-get install -y unzip libaio-dev php5-dev \
    && apt-get install -y openssl \
    && apt-get autoremove -y && apt-get clean && rm -r /var/lib/apt/lists/*

ADD instantclient/* /tmp/

RUN unzip /tmp/instantclient-basic-linux.x64-11.2.0.4.0.zip -d /usr/local/ \
    && unzip /tmp/instantclient-sdk-linux.x64-11.2.0.4.0.zip -d /usr/local/ \
    && unzip /tmp/instantclient-sqlplus-linux.x64-11.2.0.4.0.zip -d /usr/local/ \
    && rm /tmp/instantclient-*

RUN ln -s /usr/local/instantclient_11_2 /usr/local/instantclient \
    && ln -s /usr/local/instantclient/libclntsh.so.11.1 /usr/local/instantclient/libclntsh.so \
    && ln -s /usr/local/instantclient/sqlplus /usr/bin/sqlplus \
    && echo 'instantclient,/usr/local/instantclient' | pecl install oci8 \

    && echo "; priority=30\nextension=oci8.so" > /etc/php5/mods-available/oci8.ini \
    && php5enmod oci8

ENV ORACLE_HOME /usr/local/instantclient
ENV LD_LIBRARY_PATH $ORACLE_HOME
ENV PATH $ORACLE_HOME:$PATH

