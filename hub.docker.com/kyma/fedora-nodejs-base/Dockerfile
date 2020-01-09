FROM mattdm/fedora:f19
MAINTAINER Kyle Mathews "mathews.kyle@gmail.com"

# Install nodejs and npm packages.
RUN yum update -y
RUN yum install -y --skip-broken nodejs npm
# Clean up
RUN yum clean all
