FROM accur8/a8_dev:latest

MAINTAINER Accur8 Software "https://github.com/accur8"

WORKDIR /root/

RUN \
  rm -rf /etc/service/{cron,syslog-forwarder,syslog-ng} && \ 
  curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-ci-multi-runner/script.deb.sh | sudo bash && \
  apt-get install gitlab-ci-multi-runner && \
  rm -f /etc/service/sshd/down && \
  /etc/my_init.d/00_regen_ssh_host_keys.sh

#
# note you will still need to manually register this gitlab runner
#   
#   https://gitlab.com/gitlab-org/gitlab-ci-multi-runner/blob/master/docs/install/linux-repository.md
# 


COPY image/ /

CMD ["/sbin/my_init"]
