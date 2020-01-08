FROM debian:latest AS ansible

RUN apt-get update && \
    apt-get install -y \
      apt-utils ca-certificates curl dialog dnsutils gnupg2 less \
      openssh-client python-cryptography sudo traceroute vim

RUN apt-key adv --keyserver keyserver.ubuntu.com \
      --recv-keys 93C4A3FD7BB9C367 && \
    echo 'deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main' \
    > /etc/apt/sources.list.d/ansible.list && \
    apt-get update && \
    apt-get install -y ansible

RUN useradd -c "Ansible User" \
      --home-dir /home/ansible \
      --create-home \
      --uid 1000 \
      --user-group \
      --groups sudo \
      --shell /bin/bash \
      ansible && \
    echo 'ansible ALL=(ALL) NOPASSWD:ALL' > /etc/sudoers.d/ansible

RUN ( \
      echo 'eval $(ssh-agent)' && \
      echo 'if [[ -f ~/.ssh/id_ansible ]]; then ssh-add ~/.ssh/id_ansible; fi' && \
      echo 'export EDITOR=vim' \
    ) >> /home/ansible/.profile

ENTRYPOINT ["su", "-l", "ansible"]
