FROM centos:centos7

LABEL maintainer "uzresk"

ARG ANSIBLE_VERSION=2.9.2

RUN echo -e "[AdoptOpenJDK]\n\
name=AdoptOpenJDK\n\
baseurl=http://adoptopenjdk.jfrog.io/adoptopenjdk/rpm/centos/7/x86_64\n\
enabled=1\n\
gpgcheck=1\n\
gpgkey=https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public\n\
" >> /etc/yum.repos.d/adoptopenjdk.repo

RUN yum -y install epel-release \
                   python36 \
                   python36-pip \
                   python36-devel \
                   gcc-c++ \
                   gcc \
                   bzip2 \
                   openssl-devel \
                   libyaml-devel \
                   libffi-devel \
                   readline-devel \
                   zlib-devel \
                   gdbm-devel \
                   ncurses-devel \
                   make \
                   sshpass \
                   git \
                   openssl-devel \
                   iproute \
                   unzip \
                   adoptopenjdk-8-hotspot.x86_64 && \
                   rm -rf /var/cache/yum/* && \
                   yum clean all

# install ansible
RUN pip3.6 install cryptography && \
    pip3.6 install ansible==$ANSIBLE_VERSION && \
    pip3.6 install boto && \
    pip3.6 install pywinrm && \
    pip3.6 install shyaml && \
    pip3.6 install xlrd && \
    pip3.6 install pandas && \
    pip3.6 install PyVmomi

# install ruby & serverspec
ENV RBENV_ROOT /root/.rbenv
RUN git clone https://github.com/rbenv/rbenv.git $RBENV_ROOT && \
    git clone https://github.com/sstephenson/ruby-build.git $RBENV_ROOT/plugins/ruby-build
ENV PATH $PATH:$RBENV_ROOT/bin:$RBENV_ROOT/shims
RUN rbenv install 2.4.0 && \
    rbenv global 2.4.0 \
    gem install bundler && \
    gem install serverspec \
                rspec_junit_formatter \
                winrm \
                ansible-vault \
                highline \
                nokogiri

# set locale ja_JP.UTF-8, timezone
RUN localedef -v -c -i ja_JP -f UTF-8 ja_JP.UTF-8; echo "";
ENV LANG=ja_JP.UTF-8
RUN rm -f /etc/localtime
RUN ln -fs /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# set ansible.cfg
RUN mkdir -p /etc/ansible
RUN echo $'[defaults] \n\
deprecation_warnings=False\n\
command_warnings=False' > /etc/ansible/ansible.cfg
ENV ANSIBLE_CONFIG /etc/ansible/ansible.cfg


