FROM cjjcsu/centos7-openjdk

MAINTAINER cjjcsu <cjjcsu@outlook.com>

WORKDIR /opt

ENV ALLUXIO_VERSION=1.8.1

# install openssh-server
RUN rpm --rebuilddb && yum install -y openssh-server openssh-clients initscripts rsync && yum clean all

# ssh without key
ADD ssh-config /root/.ssh/config
RUN chmod 600 /root/.ssh/config
RUN chown root:root /root/.ssh/config
RUN echo "/usr/sbin/sshd" >> ~/.bashrc
RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
RUN cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
RUN /usr/bin/ssh-keygen -A

# install alluxio
RUN wget http://alluxio.org/downloads/files/${ALLUXIO_VERSION}/alluxio-${ALLUXIO_VERSION}-bin.tar.gz && \
    tar -xzvf alluxio-${ALLUXIO_VERSION}-bin.tar.gz && \
    rm alluxio-${ALLUXIO_VERSION}-bin.tar.gz

RUN ulimit -n 10240