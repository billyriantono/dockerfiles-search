FROM gear2000/chef-solo
MAINTAINER Gary Leong <gwleong@gmail.com>

############################################################
RUN echo "Running Jiffy self-contained installers" && \
    mkdir /var/tmp/jiffy

# keep upstart quiet
RUN dpkg-divert --local --rename --add /sbin/initctl && \
    ln -sf /bin/true /sbin/initctl

# no tty
ENV DEBIAN_FRONTEND noninteractive

# get up to date
RUN apt-get update --fix-missing

COPY var/tmp/docker/jiffy/tarballs/selfcontained /var/tmp/jiffy

ADD install.sh /install.sh
ADD run.sh /run.sh
#-----------
#Automated created below and added by Jiffy

RUN /install.sh 20.Base.v2.tar.gz
RUN /install.sh 30.Ubuntu_Base.v2.tar.gz
RUN /install.sh 40.Ubuntu_Base.v2.tar.gz
RUN /install.sh 50.Ubuntu_14.04_DockerInDocker_Install.v2.tar.gz
RUN /install.sh 60.Ubuntu_14.04_DockerInDocker_Install.v2.tar.gz
CMD ["/run.sh"]

#-----------