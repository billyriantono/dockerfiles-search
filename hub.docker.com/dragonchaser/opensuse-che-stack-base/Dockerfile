FROM opensuse/leap

MAINTAINER Christian Richter <crichter@suse.com>

EXPOSE 22 4403

ARG JAVA_VERSION=1_8_0

ENV JAVA_HOME=/usr
ENV PATH=$JAVA_HOME/bin:$PATH

RUN zypper ref
RUN zypper up -y
RUN zypper install -y \
    sudo \
    openssh \
    git \
    wget \
    unzip \
    mc \
    bash-completion \
    java-${JAVA_VERSION}-openjdk \
    java-${JAVA_VERSION}-openjdk-devel
RUN zypper install -y -t pattern \
    devel_basis devel_java
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config && \
    sed -ri 's/#UsePAM no/UsePAM no/g' /etc/ssh/sshd_config && \
    echo "%root ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers && \
    # Adding user to the 'root' is a workaround for https://issues.jboss.org/browse/CDK-305
    useradd -u 1000 -G users,root -d /home/user --shell /bin/bash -m user && \
    usermod -p "*" user && \
    echo 'Defaults:user !requiretty' >> /etc/sudoers

USER user
WORKDIR /projects

# The following instructions set the right
# permissions and scripts to allow the container
# to be run by an arbitrary user (i.e. a user
# that doesn't already exist in /etc/passwd)
ENV HOME /home/user
RUN for f in "/home/user" "/etc/passwd" "/etc/group" "/projects"; do\
      sudo chgrp -R 0 ${f} && \
      sudo chmod -R g+rwX ${f}; \
    done && \
    # Generate passwd.template \
    cat /etc/passwd | \
    sed s#user:x.*#user:x:\${USER_ID}:\${GROUP_ID}::\${HOME}:/bin/bash#g \
      > /home/user/passwd.template && \
    # Generate group.template \
    cat /etc/group | \
    sed s#root:x:0:#root:x:0:0,\${USER_ID}:#g \
      > /home/user/group.template && \
    sudo sed -ri 's/StrictModes yes/StrictModes no/g' /etc/ssh/sshd_config

COPY ["entrypoint.sh","/home/user/entrypoint.sh"]

ENTRYPOINT ["/home/user/entrypoint.sh"]
CMD tail -f /dev/null
