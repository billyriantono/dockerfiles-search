FROM openshift/jenkins-slave-base-centos7

MAINTAINER Ben Parees <bparees@redhat.com>

# Labels consumed by Red Hat build service
LABEL com.redhat.component="jenkins-slave-docker-python-rhel7-container" \
      name="openshift3/jenkins-slave-docker-python-rhel7" \
      version="3.6" \
      architecture="x86_64" \
      io.k8s.display-name="Jenkins Slave Docker Python" \
      io.k8s.description="The jenkins slave dockerwith python." \
      io.openshift.tags="openshift,jenkins,slave,docker,python"

# Install python 2.7.15
RUN INSTALL_PKGS="java-1.8.0-openjdk-devel.x86_64" && \
    x86_EXTRA_RPMS=$(if [ "$(uname -m)" == "x86_64" ]; then echo -n java-1.8.0-openjdk-devel.i686 ; fi) && \
    yum install -y centos-release-scl-rh && \
    yum install -y --enablerepo=centosplus $INSTALL_PKGS $x86_EXTRA_RPMS && \
    yum install gcc openssl-devel bzip2-devel -y && \
    yum groupinstall "Development Tools" -y && \
    yum clean all -y && \
    cd /usr/src && \
    wget https://www.python.org/ftp/python/2.7.15/Python-2.7.15.tgz && \
    tar xzf Python-2.7.15.tgz && \
    cd Python-2.7.15 && \
    ./configure && \
    make altinstall

# Install Doceker Bin
ADD contrib/docker-1.13.1-ce.tar.gz /usr/bin/
ADD contrib/docker /etc/sysconfig/
RUN chown -R root:root /etc/sysconfig/docker && \
    chown -R root:root /usr/bin/

# Copy slave bin
ADD contrib/bin/configure-slave /usr/local/bin/configure-slave

RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME

USER 1001
