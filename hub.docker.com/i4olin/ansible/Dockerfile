FROM debian:sid

RUN apt-get update -y && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    build-essential autoconf libtool python3 python3-dev python3-pip python3-setuptools apt-utils neovim pwgen ripgrep fzf fish tmux 

RUN pip3 install --upgrade pip setuptools wheel virtualenv
RUN pip3 install ansible==2.8.5 genie junos-eznc ansible-lint neovim jmespath

RUN mkdir /etc/ansible/ 
RUN /bin/echo -e "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts
#RUN locale-gen en_US.UTF-8

# TODO tmux.conf
# TODO ansible.cfg somewhere ( default )
# TODO .bashrc
# TODO .config/fish with functions

CMD /bin/bash
