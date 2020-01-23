FROM centos:latest

# Apply updates
RUN yum -y update

# Add the EPEL repo, for NodeJS (and probably others)
# See: https://fedoraproject.org/wiki/EPEL
RUN yum install -y epel-release

# Install St*** run deps
RUN yum install -y \
  nodejs-0.10.36   \
  python-2.7.5     \
  python-pip-7.1.0 \
  s3cmd-1.5.1.2

# Install St*** build deps
RUN yum install -y     \
  maven-3.0.5          \
  gcc-4.8.3            \
  python-devel-2.7.5   \
  mariadb-devel-5.5.44

# Clean up
RUN yum clean all
