FROM centos:7

ENV container docker

# Install tools
RUN INSTALL_PKGS="telnet \
                  bind-utils" && \
    yum install -y --setopt=tsflags=nodocs $INSTALL_PKGS --nogpgcheck && \
    rpm -V $INSTALL_PKGS && \
    yum clean all -y

CMD ["/bin/sh", "-c", "while true; do sleep 2; date; done"]
