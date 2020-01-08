FROM istoryful/centos-utf8:7
RUN yum install -y gcc-c++ make && \
    curl -sL https://rpm.nodesource.com/setup_6.x | bash - && \
    yum install -y nodejs

CMD ["/bin/bash"]
