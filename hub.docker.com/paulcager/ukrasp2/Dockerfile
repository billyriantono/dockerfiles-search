FROM centos:7

ENV BASEDIR=/root/rasp/
RUN mkdir $BASEDIR

EXPOSE 80

WORKDIR /root/rasp

# required packages
RUN yum -y update && yum -y install epel-release && yum -y update
RUN yum -y install ncl netcdf-fortran libpng15 iproute-tc tcp_wrappers-libs sendmail procmail psmisc procps-ng mailx \
  findutils ImageMagick perl-CPAN ncl netcdf libpng libjpeg-turbo which \
  zip vim wget lighttpd


RUN rpm -i http://ftp.tu-chemnitz.de/pub/linux/dag/redhat/el6/en/x86_64/rpmforge/RPMS/perl-Proc-Background-1.10-1.el6.rf.noarch.rpm

ADD src/ $BASEDIR
RUN mkdir /root/rasp/UK{4,2+1,12}/{LOG,HTML,GRIB,OUT}
ADD dotfiles/ /root/
ADD Dockerfile.centos /tmp/
#ADD libjasper.so.1 libpng15.so.15 /lib64/

CMD ["bash"]
