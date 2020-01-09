FROM    centos:centos6
MAINTAINER James Finnerty

# Enable Extra Packages for Enterprise Linux (EPEL) for CentOS
RUN     yum install -y epel-release
# Install Node.js and npm
RUN     yum install -y nodejs npm

COPY . /src

EXPOSE  8080

CMD ["node", "/src/index.js"]
