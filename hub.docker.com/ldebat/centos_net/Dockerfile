FROM centos:latest

VOLUME [ "/host" ]

RUN yum -y update && \
    yum -y install \
      vim-enhanced \
      telnet \
      net-tools \
      nc \
      bind-utils \
      openssl \
      openssh-clients \
      openldap-clients \
    && yum clean all

CMD ["bash", "-c", "while true; do echo Alive; sleep 10; done"]
