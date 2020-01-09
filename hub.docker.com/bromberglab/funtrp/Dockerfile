FROM phusion/baseimage
MAINTAINER Maximilian Miller <mmiller@bromberglab.org>

# ensure UTF-8
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

# change resolv.conf
#RUN echo 'nameserver 8.8.8.8' > /etc/resolv.conf

# setup
ENV HOME /root
RUN /etc/my_init.d/00_regen_ssh_host_keys.sh

CMD ["/sbin/my_init"]

# nginx-php installation
RUN DEBIAN_FRONTEND="noninteractive" apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
RUN DEBIAN_FRONTEND="noninteractive" add-apt-repository -y 'deb [arch=amd64,i386] https://cran.rstudio.com/bin/linux/ubuntu xenial/'
RUN DEBIAN_FRONTEND="noninteractive" apt-add-repository -y 'deb http://rostlab.org/debian/ stable main contrib non-free'
RUN DEBIAN_FRONTEND="noninteractive" apt-get update
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y --allow-unauthenticated install rostlab-debian-keyring
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y upgrade
RUN DEBIAN_FRONTEND="noninteractive" apt-get update --fix-missing
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install python3-dev libmysqlclient-dev
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install python3-setuptools python3-pip
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install python-software-properties
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install profphd
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install profbval
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install perlbrew
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install bzip2 patch
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install nano
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install wget
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install r-base
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install libssl-dev libcurl4-openssl-dev libxml2-dev
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install openjdk-8-jdk
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install tmseg rate4site
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install bc

# create rheostat project directory and copy setup files
RUN mkdir /rheostat
ADD build/bromberglab_suite /rheostat/bromberglab_suite
ADD build/src/models /rheostat/models
ADD build/src/funtrp.sh /rheostat/funtrp.sh
RUN chmod +x /rheostat/funtrp.sh
ADD build/setup.R /rheostat/setup.R

# add build script
RUN mkdir -p /root/setup
ADD build/setup.sh /root/setup/setup.sh
RUN chmod +x /root/setup/setup.sh
RUN (cd /root/setup/; /root/setup/setup.sh)

# copy files from repo
ADD build/_.bashrc /root/.bashrc

# set entrypoint
ENTRYPOINT ["/rheostat/funtrp.sh"]

# set terminal environment
ENV TERM=xterm

# cleanup apt and lists
RUN apt-get clean
RUN apt-get autoclean
