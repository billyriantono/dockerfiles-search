FROM centos:6

RUN yum install -y centos-release-scl-rh
RUN yum install -y devtoolset-7 wget git

# Clean up
RUN yum clean all

ADD entrypoint.sh /
ENTRYPOINT ["/entrypoint.sh"]
CMD ["bash"]
