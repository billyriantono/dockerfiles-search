FROM ljeczmien/php-apache-autobuild:5.4

RUN apt-get update && apt-get install -y \
    unzip

RUN chmod +x /usr/local/bin/docker-php-*

ENV ORACLE_PATH /usr/local/lib/oracle
ENV ORACLE_HOME $ORACLE_PATH/instantclient_12_1
ENV ORACLE_INSTANTCLIENT_VERSION 12.1.0.2.0
ENV ORACLE_INSTANTCLIENT_DIR oracle

# Install oracle instant client
RUN mkdir -p "$ORACLE_PATH"
COPY instantclient/instantclient-basic-linux.x64-$ORACLE_INSTANTCLIENT_VERSION.zip $ORACLE_PATH/
COPY instantclient/instantclient-sdk-linux.x64-$ORACLE_INSTANTCLIENT_VERSION.zip $ORACLE_PATH/

RUN unzip $ORACLE_PATH/instantclient-basic-linux.x64-$ORACLE_INSTANTCLIENT_VERSION -d $ORACLE_PATH/ && \
    unzip $ORACLE_PATH/instantclient-sdk-linux.x64-$ORACLE_INSTANTCLIENT_VERSION -d $ORACLE_PATH/ && \
    ln -s $ORACLE_PATH/instantclient_12_1/libclntsh.so.12.1 $ORACLE_PATH/instantclient_12_1/libclntsh.so && \
    ln -s $ORACLE_PATH/instantclient_12_1/libocci.so.12.1 $ORACLE_PATH/instantclient_12_1/libocci.so && \
    rm -r $ORACLE_PATH/*.zip
RUN docker-php-ext-configure oci8 --with-oci8=instantclient,$ORACLE_HOME \
    && docker-php-ext-install oci8