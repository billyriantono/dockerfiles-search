FROM centos:7

LABEL name="nodejs-centos" \ 
      description="Node.js running on CentOS 7." \
      maintainer="Brian Gribble <brian@83problems.com>"

# Install nodejs
RUN /usr/bin/yum -y update \
    && yum -y install epel-release \
    && /usr/bin/yum -y install nodejs npm \
    && /usr/bin/yum clean all

# Start node
CMD [ "node" ]
