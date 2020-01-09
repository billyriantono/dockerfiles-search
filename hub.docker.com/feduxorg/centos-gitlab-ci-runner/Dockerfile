FROM feduxorg/centos:latest
MAINTAINER dev@fedux.org

# ADD runner.repo /etc/yum.repos.d/runner.repo
# RUN yum install -y gitlab-runner

# Nightly
RUN yum install -y https://gitlab-ci-multi-runner-downloads.s3.amazonaws.com/master/rpm/gitlab-ci-multi-runner_amd64.rpm

# ADD gitlab-ci-runner.service /etc/systemd/system/gitlab-ci-runner.service
# RUN systemctl enable gitlab-ci-runner

RUN install -d -m 0755 -o root -g root /etc/gitlab-runner

VOLUME ["/etc/gitlab-runner"]
