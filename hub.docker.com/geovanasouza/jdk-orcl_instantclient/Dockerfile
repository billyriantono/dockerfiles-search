FROM openjdk:8

ADD instantclient-basic-linux.x64-12.2.0.1.0.zip /tmp
ADD instantclient-sqlplus-linux.x64-12.2.0.1.0.zip /tmp
ADD instantclient-tools-linux.x64-12.2.0.1.0.zip /tmp
RUN mkdir /opt/oracle && \
    unzip  /tmp/instantclient-basic-linux.x64-12.2.0.1.0.zip -d /opt/oracle && \
    unzip /tmp/instantclient-sqlplus-linux.x64-12.2.0.1.0.zip -d /opt/oracle && \
    unzip /tmp/instantclient-tools-linux.x64-12.2.0.1.0.zip -d /opt/oracle && \
    rm -f /tmp/instantclient-basic-linux.x64-12.2.0.1.0.zip /tmp/instantclient-sqlplus-linux.x64-12.2.0.1.0.zip /tmp/instantclient-tools-linux.x64-12.2.0.1.0.zip && \
    ln -s /opt/oracle/instantclient_12_2/libclntsh.so.12.1 /opt/oracle/instantclient_12_2/libclntsh.so && \
    ln -s /opt/oracle/instantclient_12_2/libocci.so.12.1 /opt/oracle/instantclient_12_2/libocci.so
RUN apt-get update && apt-get install -y libaio1 expect
ENV LD_LIBRARY_PATH=/opt/oracle/instantclient_12_2:$LD_LIBRARY_PATH
ENV PATH=/opt/oracle/instantclient_12_2:$PATH
