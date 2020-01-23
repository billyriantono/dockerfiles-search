FROM centos:7

# Install utils
RUN yum install gcc rpm-build curl git make wget binutils -y

# Install release repos
RUN yum install epel-release centos-release-scl centos-release-scl-rh -y

# Install zeromq-devel
RUN yum install zeromq-devel -y

# Install ruby
RUN yum install rh-ruby24{,-ruby-devel,-rubygem-bundler} -y

# Install python (2.6 and 2.7)
RUN yum install python{,-devel,-setuptools,-pip} python27-python{,-devel,-setuptools} -y
RUN pip install setuptools==36.8.0
RUN pip install pex==1.2.10

# Install golang
RUN wget https://storage.googleapis.com/golang/go1.11.2.linux-amd64.tar.gz --quiet
RUN tar -xf go1.11.2.linux-amd64.tar.gz
RUN cp -R go /usr/local/
RUN cp go/bin/go /usr/bin/go
RUN cp go/bin/godoc /usr/bin/godoc
RUN cp go/bin/gofmt /usr/bin/gofmt
RUN go version

# Install JDK
RUN yum install java-1.8.0-openjdk-devel -y

# Install memcached
RUN yum install memcached -y

# Other dependencies
RUN yum install -y autoconf cyrus-sasl-devel libcurl-devel libuuid-devel pcre-devel vim-enhanced automake \
gcc mysql-devel libxml2-devel libtool libpng-devel libjpeg-turbo-devel unzip bzip2 libxslt-devel \
libmcrypt-devel readline-devel openssl-devel postgresql-devel \
librabbitmq-devel kernel-headers gcc zlib-devel openssl-devel perl libcurl-devel expat-devel gettext-devel \
perl-devel perl-Time-HiRes libevent-devel tcl scl-utils scl-utils-build

# Install FPM
RUN scl enable rh-ruby24 "gem install fpm --no-ri --no-rdoc"

ENV PATH /opt/rh/rh-ruby24/root/usr/local/bin:$PATH

# Docker wrapper to fix permission issues if scripts fail/error
COPY docker_wrapper.sh /opt/docker_wrapper.sh

ENTRYPOINT ["/bin/sh", "/opt/docker_wrapper.sh"]