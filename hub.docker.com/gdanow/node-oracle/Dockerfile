FROM node:8

# set working directory to root folder
WORKDIR /

# configure apt-get
RUN apt-get update \
  && apt-get -y upgrade

# install libaio, python, zip, gcc, make & g++
RUN apt-get install python \
  && apt-get -y install zip \
  && apt-get -y install gcc \
  && apt-get -y install make \
  && apt-get -y install g++  \
  && apt-get -y install libaio1

# copy oracle files and configure oracle instantclient
RUN mkdir -p /opt/oracle
COPY instantclient* /opt/oracle/
RUN unzip /opt/oracle/instantclient-basic-linux.x64-12.2.0.1.0.zip -d /opt/oracle/ \
 && unzip /opt/oracle/instantclient-sdk-linux.x64-12.2.0.1.0.zip -d /opt/oracle/ \
 && rm /opt/oracle/instantclient-* \
 && mv /opt/oracle/instantclient_12_2 /opt/oracle/instantclient \
 && ln -s /opt/oracle/instantclient/libclntsh.so.12.1 /opt/oracle/instantclient/libclntsh.so

# set environment variable for ld_library_path, oci_lib_dir and oci_inc_dir
ENV LD_LIBRARY_PATH=/opt/oracle/instantclient:$LD_LIBRARY_PATH
ENV OCI_LIB_DIR=/opt/oracle/instantclient
ENV OCI_INC_DIR=/opt/oracle/instantclient/sdk/include

#ENV PATH=/home/node/.npm-global/bin:$PATH
#ENV NPM_CONFIG_PREFIX=/home/node/.npm-global

# install oracledb module for node
USER root
RUN chown -R node /usr/local/lib/node_modules
USER node
RUN npm install -g oracledb

# change workdirectory to /home/node
WORKDIR /home/node/

CMD [ "node" ]
