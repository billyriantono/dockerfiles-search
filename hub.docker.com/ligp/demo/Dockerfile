FROM ubuntu:14.04
MAINTAINER ligp
RUN apt-get update -q \
    && DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
      ca-certificates \
      openssh-server \
      wget \
      apt-transport-https \
      vim \
      nano
#set ENV
ENV GITLAB_HOST 192.168.31.136
# Download & Install GitLab 
# If you run GitLab Enterprise Edition point it to a location where you have downloaded it. 
#RUN echo "deb https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/ubuntu xenial main" > /etc/apt/sources.list.d/gitlab_gitlab-ce.list
RUN echo "deb https://mirrors.tuna.tsinghua.edu.cn/gitlab-ce/ubuntu trusty main" > /etc/apt/sources.list.d/gitlab_gitlab-ce.list
#RUN echo "deb https://packages.gitlab.com/gitlab/gitlab-ce/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/gitlab_gitlab-ce.list
RUN wget -q -O - https://packages.gitlab.com/gpg.key | apt-key add -
RUN apt-get update || ture &&  apt-get install -y gitlab-ce=10.1.0-ce.0
# Manage SSHD through runit 
RUN mkdir -p /opt/gitlab/sv/sshd/supervise \
    && mkfifo /opt/gitlab/sv/sshd/supervise/ok \
    && printf "#!/bin/sh\nexec 2>&1\numask 077\nexec /usr/sbin/sshd -D" > /opt/gitlab/sv/sshd/run \
    && chmod a+x /opt/gitlab/sv/sshd/run \
    && ln -s /opt/gitlab/sv/sshd /opt/gitlab/service \
    && mkdir -p /var/run/sshd
# Disabling use DNS in ssh since it tends to slow connecting 
RUN echo "UseDNS no" >> /etc/ssh/sshd_config
# Prepare default configuration 
RUN ( \
  echo "" && \
  echo "# Docker options" && \
  echo "# Prevent Postgres from trying to allocate 25% of total memory" && \
  echo "postgresql['shared_buffers'] = '1MB'" ) >> /etc/gitlab/gitlab.rb && \
  mkdir -p /assets/ && \
  cp /etc/gitlab/gitlab.rb /assets/gitlab.rb
# Expose web & ssh 
EXPOSE 443 80 22
# Define data volumes 
VOLUME ["/etc/gitlab", "/var/opt/gitlab", "/var/log/gitlab"]
# Copy assets 
COPY wrapper /usr/local/bin/
RUN chmod 777 /usr/local/bin/wrapper
COPY RELEASE /
# Wrapper to handle signal, trigger runit and reconfigure GitLab 
CMD ["/usr/local/bin/wrapper"]
