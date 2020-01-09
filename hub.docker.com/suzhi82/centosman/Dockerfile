FROM centos:7
RUN sed -i 's/tsflags=nodocs/# tsflags=nodocs/g' /etc/yum.conf &&\
    yum install -y man man-db man-pages
CMD ["/bin/bash"]
