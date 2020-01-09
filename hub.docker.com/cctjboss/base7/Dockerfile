FROM centos:7
MAINTAINER David Becvarik <dbevari@redhat.com>

# Install packages necessary to run EAP
RUN yum -y install python python-devel python-setuptools unzip git gcc libxml2-devel libxslt-devel && yum clean all

# Install cct
RUN git clone https://github.com/containers-tools/cct && \
    cd cct && \
    easy_install .

# Create a user and group used to launch processes
# The user ID 1000 is the default for the first "regular" user on Fedora/RHEL,
# so there is a high chance that this ID will be equal to the current user
# making it easier to use volumes (no permission issues)
RUN groupadd -r jboss -g 1000 && useradd -u 1000 -r -g jboss -m -d /opt/jboss -s /sbin/nologin -c "JBoss user" jboss && \
    chmod 755 /opt/jboss

# Set the working directory to jboss' user home directory
WORKDIR /opt/jboss

# Specify the user which should be used to execute all commands below
USER jboss

ENTRYPOINT ["/usr/bin/cct", "-c"]
CMD ["bash"]
