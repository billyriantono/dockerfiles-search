FROM sequenceiq/hadoop-docker:2.7.1 

RUN yum -y --enablerepo=extras install epel-release && \
    yum -y clean all && \
    yum -y install python-pip wget nano vim && \
    yum -y clean all

RUN pip install google-api-python-client==1.6.4 && \
    pip install mrjob==0.5.11

COPY assets/.bashrc /root/

ENV PATH=$PATH:$HADOOP_PREFIX/bin
