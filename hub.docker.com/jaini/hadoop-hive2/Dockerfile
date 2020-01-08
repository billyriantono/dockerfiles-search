#It is work of mycrypt/hadoop-hive (Bai Xiaoyong lostitle@gmail.com), I've updated hive version to 2.0

FROM mycrypt/hadoop
MAINTAINER Amit Jain aj2011it@gmail.com

RUN mkdir /opt/hive
RUN wget -qO- http://mirror.fibergrid.in/apache/hive/hive-2.0.0/apache-hive-2.0.0-bin.tar.gz \
  | tar zxvf - -C /opt/hive --strip 1

RUN cp /opt/hive/conf/hive-default.xml.template /opt/hive/conf/hive-default.xml && \
    cp /opt/hive/conf/hive-default.xml.template /opt/hive/conf/hive-site.xml && \
    cp /opt/hive/conf/hive-env.sh.template /opt/hive/conf/hive-env.sh && \
    cp /opt/hive/conf/hive-log4j2.properties.template /opt/hive/conf/hive-log4j2.properties

ENV PATH /opt/hive/bin:$PATH

RUN echo "\n\
export HIVE_HOME=/opt/hive\n\
PATH=$HIVE_HOME/bin:$PATH\
\n\
" >> /etc/profile