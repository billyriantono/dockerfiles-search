FROM centos:7
#Install java
RUN yum -y install java-1.8.0-openjdk.x86_64 wget.x86_64 && \
    #Changing timezone
    rm -rf /etc/localtime && \
    ln -s /usr/share/zoneinfo/Europe/Kiev /etc/localtime
CMD ["/bin/bash"]

