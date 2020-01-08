# ------------------------------------------------------
#                       Dockerfile
# ------------------------------------------------------
# image:    ansible-ddg-hack
# tag:      latest
# name:     ansibleshipyard/ansible-ddg-hack
# version:  1.0.0
# repo:     https://github.com/ansibleshipyard/ansible-ddg-hack
# how-to:   docker build --force-rm -t ansibleshipyard/ansible-ddg-hack .
# run:      docker run -t -i -u ddghacker $DOCKERNAME bash
# requires: ansible-base-ubuntu
# authors:  jason.giedymin@gmail.com
# desc: Ansible playbook to install duck duck go's hack environment.
# Created via Ansible CI/Docker Playbook Generator
# ------------------------------------------------------

FROM ansibleshipyard/ansible-base-ubuntu
MAINTAINER ansibleshipyard

# -----> Env
ENV WORKDIR /tmp/build/roles/ansible-ddg-hack
WORKDIR /tmp/build/roles/ansible-ddg-hack

# -----> Add assets
ADD ./defaults $WORKDIR/defaults
ADD ./handlers $WORKDIR/handlers
ADD ./meta $WORKDIR/meta
ADD ./tasks $WORKDIR/tasks
ADD ./templates $WORKDIR/templates
ADD ./vars $WORKDIR/vars
ADD ./ci $WORKDIR/ci

# -----> Install Galaxy Dependencies

# -----> Execute
RUN ansible-playbook -i $WORKDIR/ci/inventory $WORKDIR/ci/playbook.yml -c local -vvvv

# -----> Cleanup
WORKDIR /
RUN rm -R /tmp/build
