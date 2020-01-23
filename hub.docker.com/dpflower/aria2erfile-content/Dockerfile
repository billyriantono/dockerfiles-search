FROM centos:7
LABEL maintainer="Dovry"
ENV container=docker
ENV script_url "https://raw.githubusercontent.com/Dovry/ansible-install-script/master/ansible_convenience_script.sh"

# Install required packages
RUN yum makecache fast \
  && yum -y install wget \
# Install ansible
  && wget $script_url \
  && chmod +x ansible_convenience_script.sh \
  && sh ./ansible_convenience_script.sh -p \
  && rm -f ansible_convenience_script.sh \
  && yum clean all

VOLUME ["/sys/fs/cgroup"]
CMD ["/usr/lib/systemd/systemd"]
HEALTHCHECK CMD ansible --version