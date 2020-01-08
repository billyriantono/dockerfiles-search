FROM centos
LABEL maintainer=jooool

RUN yum install ansible -y

# So ansible-galaxy init can permanently write data let's work in /tmp instead of /
# Also it helps to avoid path for playbook and hosts while calling ansible-playbook
WORKDIR /tmp

# The below entry can be override w/ ansible-playbook, ansible-galaxy, etc
ENTRYPOINT ["ansible"]
