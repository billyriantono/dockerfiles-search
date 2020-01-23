FROM centos

RUN yum install -y wget \
  && cd /etc/yum.repos.d/ \
  && wget http://mirrors.163.com/.help/CentOS6-Base-163.repo \
  && sed -i 's#$releasever#6#g' CentOS6-Base-163.repo \
  && yum clean all && yum makecache fast  && yum update -y \
  && yum install -y  gcc-c++ pcre pcre-devel zlib zlib-devel  openssl openssl-devel \
  && yum clean all

RUN wget https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.22.0.tar.gz \
  && tar -zxf git-2.22.0.tar.gz && mv git-2.22.0 /usr/local/src/git-2.22.0  && rm -f git-2.22.0.tar.gz \
  && yum install -y curl-devel expat-devel gettext-devel openssl-devel zlib-devel \
  && yum install -y gcc perl-ExtUtils-MakeMaker \
  && cd  /usr/local/src/git-2.22.0 && ./configure --prefix=/usr/local/git \
  $$ make && make install

ENV JAVA_VERSION="1.8.0_141"

ENV JAVA_HOME="/usr/local/src/jdk${JAVA_VERSION}"

ENV PATH="${PATH}:${JAVA_HOME}/bin"

RUN  mkdir -p /usr/local/src && yum install -y wget \
  && wget --no-cookies --no-check-certificate --header \
   "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" \
   "http://download.oracle.com/otn-pub/java/jdk/8u141-b15/336fa29ff2bb4ef291e347e091f7f4a7/jdk-8u141-linux-x64.tar.gz" \
  && tar -xzf jdk-8u141-linux-x64.tar.gz && mv jdk${JAVA_VERSION} /usr/local/src/ && rm -f jdk-8u141-linux-x64.tar.gz

RUN wget http://nginx.org/download/nginx-1.8.1.tar.gz \
  && tar -zxvf nginx-1.8.1.tar.gz && rm -f nginx-1.8.1.tar.gz  && cd nginx-1.8.1 \
  && ./configure --prefix=/usr/src/nginx --with-http_stub_status_module --with-http_ssl_module \
  && make && make install \
  && cd /usr/src/nginx/sbin \
  && ./nginx -v \
  && echo "/usr/src/nginx/sbin/nginx" >> /etc/rc.local \
  && cd /usr/src/nginx/sbin && ./nginx \
  && rm -rf /nginx-1.8.1

RUN wget https://nodejs.org/dist/v10.15.0/node-v10.15.0-linux-x64.tar.xz \
  && tar -xvf node-v10.15.0-linux-x64.tar.xz && rm -f node-v10.15.0-linux-x64.tar.xz \
  && mv node-v10.15.0-linux-x64 /usr/local/node-v10.15.0 \
  && ln -s /usr/local/node-v10.15.0/bin/node /usr/local/bin/node \
  && ln -s /usr/local/node-v10.15.0/bin/npm /usr/local/bin/npm \
  && ln -s /usr/local/node-v10.15.0/bin/npx /usr/local/bin/npx \
  && node -v && npm -v && npx -v

ENV MAVEN_HOME="/usr/local/maven3"\
  PATH="$MAVEN_HOME/bin:$PATH"
RUN wget http://mirror.bit.edu.cn/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz \
  && tar -zxvf apache-maven-3.3.9-bin.tar.gz \
  && mv apache-maven-3.3.9 /usr/local/maven3  && rm -f apache-maven-3.3.9-bin.tar.gz \
  && touch /etc/profile.d/mvn.sh \
  && echo "export MAVEN_HOME=/usr/local/maven3" >> /etc/profile.d/mvn.sh \
  && echo "export PATH=$MAVEN_HOME/bin:$PATH" >> /etc/profile.d/mvn.sh \
  && source /etc/profile \
  && rm -f /usr/local/maven3/conf/settings.xml
COPY ./settings.xml  /usr/local/maven3/conf/settings.xml
