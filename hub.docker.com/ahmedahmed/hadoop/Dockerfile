From java

RUN adduser --disabled-password --gecos "" hadoop
RUN apt-get update && apt-get install -y software-properties-common openssh-client vim 
#RUN ssh-keygen -t rsa
#Run cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
#RUN chmod 0600 ~/.ssh/authorized_keys


# Install oracle jdk 8
## https://askubuntu.com/questions/190582/installing-java-automatically-with-silent-option
#RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
#    echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections
#RUN mkdir -p /var/cache/oracle-jdk8-installer && \
#    echo "noclobber = off" >> /var/cache/oracle-jdk8-installer/wgetrc && \
#    echo "dir_prefix = ." >> /var/cache/oracle-jdk8-installer/wgetrc && \
#    echo "dirstruct = off" >> /var/cache/oracle-jdk8-installer/wgetrc && \
#    echo "verbose = off" >> /var/cache/oracle-jdk8-installer/wgetrc
#
#RUN add-apt-repository ppa:webupd8team/java && apt-get update && apt-get install -qq -y oracle-java8-installer
# end Install oracle jdk 8
RUN apt-get install -y openssh-client openssh-server
RUN ssh-keygen -q -t rsa -N '' -f /root/.ssh/id_rsa
RUN cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
RUN chmod 0600 ~/.ssh/authorized_keys
RUN service ssh restart
#hadoop 
RUN wget http://apache.claz.org/hadoop/common/hadoop-2.6.5/hadoop-2.6.5.tar.gz
RUN tar xzf hadoop-2.6.5.tar.gz
RUN mv hadoop-2.6.5/ hadoop
#RUN echo "export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64" >> ~/.bashrc
#RUN echo "export HADOOP_HOME=/hadoop"  >> ~/.bashrc
#RUN echo "export PATH=\$PATH:\$JAVA_HOME/bin:\$HADOOP_HOME/bin" >> ~/.bashrc
COPY .bashrc /root/.bashrc
COPY core-site.xml /hadoop/etc/hadoop/core-site.xml
COPY hdfs-site.xml /hadoop/etc/hadoop/hdfs-site.xml
COPY mapred-site.xml /hadoop/etc/hadoop/mapred-site.xml
COPY yarn-site.xml /hadoop/etc/hadoop/yarn-site.xml
COPY hadoop-env.sh /hadoop/etc/hadoop/hadoop-env.sh
COPY docker-entrypoint.sh /usr/local/bin/
EXPOSE 50070 9000 50030 8088 
#ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["bash"]

