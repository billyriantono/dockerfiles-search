#Chris Green

#install clamav
FROM centos:7
RUN yum -y update

#clamav sophos starts at wget
WORKDIR  /root/
RUN  yum -y install epel-release \
&& yum -y install clamav \
&& yum -y install wget \
&& wget https://github.com/maliceio/malice-av/raw/master/sophos/sav-linux-free-9.tgz \
&& tar xzvf sav-linux-free-9.tgz \
&& ./sophos-av/install.sh /opt/sophos --update-free --acceptlicence --autostart=False --enableOnBoot=False --automatic --ignore-existing-installation --update-source-type=s
