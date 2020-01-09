FROM solitudo/cloud9

# MySQL
RUN yum -y install https://dev.mysql.com/get/mysql80-community-release-el7-1.noarch.rpm \
  && yum-config-manager --disable mysql80-community \
  && yum-config-manager --enable mysql56-community \
  && yum -y install mysql-community-client mysql-community-devel

# Ruby
RUN yum -y install openssl-devel readline-devel sqlite-devel
RUN git clone git://github.com/sstephenson/rbenv.git /usr/local/src/rbenv \
  && git clone git://github.com/sstephenson/ruby-build.git /usr/local/src/rbenv/plugins/ruby-build \
  && git clone https://github.com/sstephenson/rbenv-default-gems.git /usr/local/src/rbenv/plugins/rbenv-default-gems \
  && git clone https://github.com/rkh/rbenv-update.git /usr/local/src/rbenv/plugins/rbenv-update
COPY rbenv/default-gems /usr/local/src/rbenv/default-gems
COPY rbenv/rbenv.sh /etc/profile.d/rbenv.sh
RUN . /etc/profile.d/rbenv.sh && rbenv install 2.5.5
RUN . /etc/profile.d/rbenv.sh && rbenv install 2.6.3

# AWS
RUN yum -y install python2-pip python34-pip \
  && pip install --upgrade pip
RUN pip install awscli \
  && curl -sSL -o /usr/local/bin/ecs-cli https://s3.amazonaws.com/amazon-ecs-cli/ecs-cli-linux-amd64-latest \
  && chmod 755 /usr/local/bin/ecs-cli

# Tools
RUN npm install -g yarn
RUN yum -y install jq

RUN yum -y clean all && rm -rf /var/cache/yum /tmp/*
