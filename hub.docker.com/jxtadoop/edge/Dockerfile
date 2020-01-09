FROM jxtadoop/java

MAINTAINER Franck Besnard <franck@besnard.mobi>

RUN apt-get install -y vim
RUN apt-get install -y unzip

RUN cd /root; wget http://downloads.sourceforge.net/project/jxtadoop/jxtadoop-1.0.0-namenode.zip
RUN cd /root;wget http://downloads.sourceforge.net/project/jxtadoop/jxtadoop-1.0.0-datanode.zip

RUN cd /opt; unzip /root/jxtadoop-1.0.0-namenode.zip
RUN cd /opt; unzip -o /root/jxtadoop-1.0.0-datanode.zip

RUN cd /opt/jxtadoop-1.0.0/etc; rm -f hdfs-p2p.xml; wget https://downloads.sourceforge.net/project/jxtadoop/hdfs-p2p.xml
