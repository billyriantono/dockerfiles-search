FROM centos:7

# Install utils
RUN yum install gcc rpm-build curl git make wget binutils -y

# Install release repos
RUN yum install epel-release centos-release-scl centos-release-scl-rh -y

# Install zeromq-devel
RUN yum install zeromq-devel -y

# Install ruby
RUN yum install rh-ruby24{,-ruby-devel} -y

# Install python
RUN yum install python{,-devel,-setuptools,-pip} -y
RUN pip install setuptools==36.8.0
RUN pip install pex==1.2.10

# Install golang
RUN wget https://storage.googleapis.com/golang/go1.11.1.linux-amd64.tar.gz --quiet
RUN tar -xf go1.11.1.linux-amd64.tar.gz
RUN cp -R go /usr/local/
RUN cp go/bin/go /usr/bin/go
RUN cp go/bin/godoc /usr/bin/godoc
RUN cp go/bin/gofmt /usr/bin/gofmt
RUN go version

# Install FPM
RUN scl enable rh-ruby24 "gem install fpm --no-ri --no-rdoc"

ENV PATH /opt/rh/rh-ruby24/root/usr/local/bin:$PATH

ENTRYPOINT ["scl", "enable", "rh-ruby24"]