FROM ansible/ansible-runner:1.4.4

RUN set -x && \
    yum install -y https://centos7.iuscommunity.org/ius-release.rpm && yum update -y --exclude='ansible*' && \
    yum install -y git jq python2-pip tree unzip wget && \
    rm -rf /var/cache/yum/* && yum clean all && \
    pip install --upgrade pip && \
    pip install ansible-lint awscli boto pywinrm yamllint && \
    mkdir -p /etc/ansible && chmod 755 /etc/ansible
