FROM centos:latest

RUN yum -y update && \ 
    yum -y install htop git iotop iftop 

RUN mkdir test
RUN touch /test/newfile 

RUN echo 'this is a new container ' > /test/newfile

CMD ["/bin/bash"]

