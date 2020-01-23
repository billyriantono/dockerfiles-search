# This is the Dockerfile that builds an image which will be used by most other
# images in the repo as their base image

FROM registry.centos.org/centos/centos

RUN yum -y update && \
    yum -y install sudo && \
    yum clean all && \
    echo "%wheel ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    useradd -u 1000 -G users,wheel -d /home/user --shell /bin/bash -m user && \
    usermod -p "*" user && \
    sed -i 's/requiretty/!requiretty/g' /etc/sudoers 

USER user

WORKDIR /home/user

CMD ["tail", "-f", "/dev/null"]
