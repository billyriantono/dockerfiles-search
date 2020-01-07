FROM gocd/gocd-agent-centos-7:v18.6.0

RUN yum install -y yum install gcc-c++ patch readline readline-devel zlib zlib-devel \
   libyaml-devel libffi-devel openssl-devel make which tar wget\
   bzip2 autoconf automake libtool bison iconv-devel sqlite-devel freetype fontconfig
 
RUN runuser -l go -c 'gpg2 --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB'
RUN runuser -l go -c 'curl -sSL https://get.rvm.io | bash -s stable'
RUN runuser -l go -c 'rvm install 2.5 && rvm use 2.5 --default && gem install bundle --no-ri --no-rdoc'

RUN cd /tmp && \
    wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2 && \
    tar xvf phantomjs-2.1.1-linux-x86_64.tar.bz2 && \
    mkdir -p /opt/phantomjs && \
    cp  phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin && \
    rm -rf /tmp/phantomjs-2.1.1-linux-x86_64*
