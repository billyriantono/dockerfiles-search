# INSTALL NODE 8.9 LTS
FROM node:carbon

RUN apt-get update \
  && apt-get install -y libaio1 \
  && apt-get install -y unzip

#ADD ORACLE INSTANT CLIENT
RUN mkdir -p opt/oracle
COPY ./oracle/linux/ .

RUN unzip instantclient-basiclite-linux.x64-12.2.0.1.0.zip -d /opt/oracle \
  && mv /opt/oracle/instantclient_12_2 /opt/oracle/instantclient \
  && rm instantclient-basiclite-linux.x64-12.2.0.1.0.zip

RUN echo '/opt/oracle/instantclient/' | tee -a /etc/ld.so.conf.d/oracle_instant_client.conf \
    && ldconfig

RUN npm_config_unsafe_perm=true npm i -g oracledb
