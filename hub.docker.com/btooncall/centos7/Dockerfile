FROM centos:7

RUN yum -y update && yum -y upgrade && yum clean all 
RUN yum -y install wget java-1.7.0-openjdk apr && yum clean all 

# stuff needed during devel and testing but not really in live
RUN yum -y install telnet net-tools nmap-ncat vim lsof && yum clean all 
