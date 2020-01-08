FROM openshift/jenkins-slave-base-centos7


RUN yum makecache && \
    yum install -y centos-release-scl && \
    yum install -y rh-python36 && \
    yum groupinstall -y 'Development Tools' && \
    yum clean all -y

RUN scl enable rh-python36 bash

RUN python --version

RUN python -m venv $HOME/venv && \
    . $HOME/venv/bin/activate && \
    pip install -U pip

ENV ENV $HOME/venv/bin/activate
ENV BASH_ENV $HOME/venv/bin/activate

RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME
    
USER 1001
