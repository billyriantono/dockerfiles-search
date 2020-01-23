FROM centos:8
MAINTAINER hackyo <137120918@qq.com>
ADD https://raw.githubusercontent.com/hackyoMa/docker-centos/8/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo
RUN rm -f CentOS-AppStream.repo CentOS-PowerTools.repo CentOS-centosplus.repo CentOS-Extras.repo && yum makecache && yum -y update && yum -y autoremove && rm -rf /var/cache/yum
CMD ["/bin/bash"]
