FROM dclong/hive

ARG hive=hive-2.1.0
ARG spark=spark-2.2.0-bin-hadoop2.7

RUN wget http://d3kbcqa49mib13.cloudfront.net/${spark}.tgz -O /${spark}.tgz \
    && tar -zxvf /${spark}.tgz -C /opt/ \
    && ln -s /opt/${spark} /usr/lib/spark \
    && ln -s /opt/apache-${hive}-bin/conf/hive-site.xml /opt/${spark}/conf/ \
    && rm /${spark}.tgz \
    && apt-get autoremove \
    && apt-get autoclean

