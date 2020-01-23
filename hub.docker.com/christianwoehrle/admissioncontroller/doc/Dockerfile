FROM jenkins 

ENV JAVA_OPTS="-DLC_CTYPE=UTF-8 -Dfile.encoding=UTF-8 $JAVA_OPTS"
ENV MAVEN_OPTS="-Doracle.jdbc.timezoneAsRegion=false"

USER root

RUN apt-get update && apt-get install -y git 
RUN apt-get install -y --force-yes maven

ENV GIT_SSL_NO_VERIFY=1

ADD ./instantclient-basic-linux.x64-12.1.0.2.0.zip /tmp/instantclient-basic-linux.x64-12.1.0.2.0.zip

RUN apt-get install -y unzip
RUN mkdir -p /opt/oracle/instantclient_12_1
RUN unzip /tmp/instantclient-basic-linux.x64-12.1.0.2.0.zip -d /opt/oracle/instantclient_12_1
RUN ln -s libclntsh.so.12.1 /opt/oracle/instantclient_12_1/libclntsh.so.12.1
RUN ln -s libocci.so.12.1 /opt/oracle/instantclient_12_1/libocci.so.12.1

RUN chown -R jenkins /opt/oracle/instantclient_12_1

ENV LD_LIBRARY_PATH /opt/oracle/instantclient_12_1:$LD_LIBRARY_PATH
ENV PATH /opt/oracle/instantclient_12_1:$PATH

USER jenkins



