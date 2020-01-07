FROM java
MAINTAINER nrstott@gmail.com

RUN curl -s http://d3kbcqa49mib13.cloudfront.net/spark-1.4.0-bin-hadoop1-scala2.11.tgz | tar -xz -C /usr/local/
RUN cd /usr/local && ln -s spark-1.4.0-bin-hadoop1-scala2.11 spark
ENV SPARK_HOME /usr/local/spark

# Add script to help start a standalone master
ADD start-master-foreground.sh /usr/local/spark/sbin/start-master-foreground.sh

RUN chmod +x /usr/local/spark/sbin/start-master-foreground.sh

CMD ["bash"]
