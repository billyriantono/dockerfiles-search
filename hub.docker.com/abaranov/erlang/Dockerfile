FROM        fedora:latest
MAINTAINER  abaranov@linux.com

RUN         yum makecache
RUN         yum -y update
RUN         yum -y install ansible git
ADD         hosts /etc/ansible/hosts
ADD         erlang.yml /ansible/erlang.yml
RUN         ansible-playbook /ansible/erlang.yml
RUN         rm -rf /ansible
RUN         mkdir /erlang
WORKDIR     /erlang

ENTRYPOINT exec /usr/bin/erl
