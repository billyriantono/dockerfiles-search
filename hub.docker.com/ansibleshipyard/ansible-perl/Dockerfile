# ------------------------------------------------------
#                       Dockerfile
# ------------------------------------------------------
# image:    ansible-perl
# tag:      latest
# name:     ansibleshipyard/ansible-perl
# version:  1.0.0
# repo:     https://github.com/ansibleshipyard/ansible-perl
# how-to:   docker build --force-rm -t ansibleshipyard/ansible-perl .
# run:      docker run -t -i $DOCKERNAME bash
# requires: ansible-base-ubuntu
# authors:  jason.giedymin@gmail.com
# desc: Ansible playbook to install perl.
# Created via Ansible CI/Docker Playbook Generator
# ------------------------------------------------------

FROM ansibleshipyard/ansible-base-ubuntu
MAINTAINER ansibleshipyard

# -----> Env
ENV WORKDIR /tmp/build/roles/ansible-perl
WORKDIR /tmp/build/roles/ansible-perl

# -----> Add assets
ADD ./defaults $WORKDIR/defaults
ADD ./handlers $WORKDIR/handlers
ADD ./meta $WORKDIR/meta
ADD ./tasks $WORKDIR/tasks
ADD ./vars $WORKDIR/vars
ADD ./ci $WORKDIR/ci

# -----> Install Galaxy Dependencies

# -----> Execute
RUN ansible-playbook -i $WORKDIR/ci/inventory $WORKDIR/ci/playbook.yml -c local -f 10 -vvvv

# -----> Cleanup
WORKDIR /
RUN rm -R /tmp/build
