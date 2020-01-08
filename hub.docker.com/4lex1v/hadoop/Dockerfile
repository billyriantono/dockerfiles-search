FROM 4lex1v/oracle-jre-8:72
MAINTAINER  Aleksandr Ivanov <4lex1v@gmail.com>

ARG HADOOP_V=2.7.1

USER root

ENV HADOOP_HOME=/opt/hadoop
ENV PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin

## Configure SSH
RUN apt-get update && apt-get install openssh-server -y && \
    ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa && \
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
    
## Install Hadoop
RUN wget http://www.eu.apache.org/dist/hadoop/common/hadoop-${HADOOP_V}/hadoop-${HADOOP_V}.tar.gz -O /tmp/hadoop.tar.gz && \
    tar xf /tmp/hadoop.tar.gz -C /tmp && \
    rm /tmp/hadoop.tar.gz && \
    mv /tmp/hadoop-${HADOOP_V} $HADOOP_HOME

## Remove old configuration library
## And replace it with local configuration
RUN rm -rf $HADOOP_HOME/etc/hadoop
ADD ./hadoop/psevdo $HADOOP_HOME/etc/hadoop


ADD ./launch.sh /launch
RUN chown root:root /launch && \
    chmod 700 /launch

ENTRYPOINT ["/launch"]
CMD ["--quite"]