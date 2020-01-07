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

RUN /install.sh 10005.Base.v1.tar.gz
RUN /install.sh 10010.Ubuntu_Base.v1.tar.gz
RUN /install.sh 10015.Ubuntu_Apache_Django.v1.tar.gz
CMD ["/run.sh"]

#-----------