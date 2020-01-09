# Dockerfile for NetKernel 5 SE
FROM databliss/ubuntu-java8-oracle
MAINTAINER Randolph Kahle "randolph.kahle@databliss.net"
ENV REFRESHED_AT 2017-06-15 

COPY netkernel /opt/netkernel 

# Estblish local user 'netkernel' and get ready to run NetKernel
RUN adduser netkernel --disabled-password --gecos '' &&\
    chown -R netkernel:netkernel /opt/netkernel &&\
    adduser netkernel sudo &&\
    echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
EXPOSE 1060
EXPOSE 8080
USER netkernel:netkernel
ENTRYPOINT ["/opt/netkernel/bin/netkernel.sh"]