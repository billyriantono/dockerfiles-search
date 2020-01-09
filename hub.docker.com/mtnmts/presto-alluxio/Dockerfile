FROM prestosql/presto

RUN curl https://downloads.alluxio.io/downloads/files/1.8.1/alluxio-1.8.1-hadoop-2.9-bin.tar.gz -o /tmp/presto.tar.gz
RUN cd /tmp && tar -xzf /tmp/presto.tar.gz 
RUN ls -laR /tmp/
RUN cp /tmp/alluxio-1.8.1-hadoop-2.9/client/alluxio-1.8.1-client.jar /usr/lib/presto/plugin/hive-hadoop2

