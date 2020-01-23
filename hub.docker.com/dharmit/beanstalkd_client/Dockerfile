FROM registry.centos.org/dharmit/base

RUN sudo yum install -y PyYAML && \
    sudo yum install -y epel-release && \
    sudo yum install -y ipython && \
    sudo yum clean all

CMD ["tail", "-f", "/dev/null"]
