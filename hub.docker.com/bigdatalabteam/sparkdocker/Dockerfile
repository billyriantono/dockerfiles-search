FROM centos:7


RUN yum -y update \
    && yum -y install epel-release \
    && yum -y install https://centos7.iuscommunity.org/ius-release.rpm \
    && yum -y install gcc \
    && yum -y install \
        python35u \
        python35u-devel \
        python35u-pip \
    && yum -y install wget \
    && yum -y install which \
    && yum -y install vim \
    && yum -y install java-1.8.0-openjdk

RUN yum -y reinstall glibc-common \
    && localedef -i en_CA -f UTF-8 en_CA.UTF-8

RUN useradd -ms /bin/bash soen
USER soen
WORKDIR /home/soen
RUN wget -qO- http://apache.mirror.globo.tech/spark/spark-2.4.0/spark-2.4.0-bin-hadoop2.7.tgz | tar xzv

RUN export JAVA_HOME=`readlink -f $(which java)`

ENV SPARK_HOME /home/soen/spark-2.4.0-bin-hadoop2.7
ENV PATH $PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin

RUN pip3.5 install --user virtualenv \
    && python3.5 -m virtualenv labenv --python=python3.5 \
    && . labenv/bin/activate && pip install pyspark pytest dask[complete] \
    && echo 'source labenv/bin/activate' >> /home/soen/.bashrc

ENTRYPOINT ["/bin/bash"]
