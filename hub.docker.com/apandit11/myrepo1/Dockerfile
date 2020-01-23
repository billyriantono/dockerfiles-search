FROM centos:7
RUN yum update &&  yum install -y vim \
                                      which \
                                      nano
CMD ["ping", "127.0.0.1", "-c", "10"]
