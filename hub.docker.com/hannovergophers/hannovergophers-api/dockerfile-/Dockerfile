FROM python:2.7.9
MAINTAINER Derek Rowland derek.a.rowland@gmail.com

RUN apt-get update && \
    apt-get install -y git && \
    rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/gx1400/Nest_mysql_datalogger

#ADD info.config /
#ADD Nest_mysql_datalogger /nestlogger/

RUN pip install requests python-dateutil configparser mysql-connector==2.1.4

ADD startlogger.py /Nest_mysql_datalogger/

ENV NESTUSER nest_user_def
ENV NESTPW nest_pwd_def
ENV DBADDR db_addr_def
ENV DBPORT db_port_def
ENV DBUSER db_user_def
ENV DBPASS db_pass_def
ENV DBSCHEMA db_schema_def

ENTRYPOINT "./Nest_mysql_datalogger/startlogger.py" && /bin/bash