FROM centos:7
MAINTAINER Anmol J. Hemrom, anmoljh@gmail.com

RUN yum install -y epel-release && \
    yum groupinstall -y "Development Tools" && \
    yum install -y python-virtualenv python-pip tree wget vim

RUN groupadd -r -g 1000 dentos && useradd -r -g dentos -u 1000 -m dentos
USER dentos
WORKDIR /home/dentos

CMD ["/bin/bash"]
