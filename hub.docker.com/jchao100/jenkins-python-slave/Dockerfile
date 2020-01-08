FROM openshift/jenkins-slave-base-centos7

# install "Inline with Upstream Stable" to get most current upstream stable release of Python 3
RUN yum -y install https://centos7.iuscommunity.org/ius-release.rpm

# install Python 3.6 with pip
RUN yum install -y python36u python36u-pip
RUN pip3.6 install virtualenv
RUN pip3.6 install virtualenvwrapper
RUN yum -y install python36u-devel

RUN python3.6 --version

# change user to non-root OpenShift usage
RUN chown -R 1001:0 $HOME && \
    chmod -R g+rw $HOME
    
USER 1001
