FROM centos
MAINTAINER David Hollis "dhollis@raybeam.com"

# Install prerequisite packages for chef
RUN yum groupinstall -y "Development Tools"
RUN yum install -y libxml2-devel libxslt-devel git

# Install chef
RUN curl -L https://www.opscode.com/chef/install.sh | bash