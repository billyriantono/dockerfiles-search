# docker image for automatic build
FROM centos:7
RUN mkdir /home/newimage
RUN cd /home/newimage
RUN yum install -y httpd
CMD ["bin/bash" , "-c" , "echo Hello,$SHELL"]
