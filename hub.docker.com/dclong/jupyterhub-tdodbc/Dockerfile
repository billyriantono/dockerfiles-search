FROM dclong/jupyterhub-jdk

ADD scripts /scripts

RUN apt-get update -y \
    && apt-get install -y \
        /scripts/tdodbc1620.deb \
    && rm -rf /scripts/tdodbc1620.deb \
    && apt-get autoremove \
    && apt-get autoclean

RUN pip3 install \
    teradata sqlalchemy-teradata jaydebeapi
    
# ADD settings /etc
ENV ODBCHOME=/opt/teradata/client/ODBC_64 ODBCINI=/opt/teradata/client/ODBC_64/odbc.ini
