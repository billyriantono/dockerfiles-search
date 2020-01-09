FROM astj/centos5-vault
WORKDIR /root

# setup repository
RUN yum install -y wget
RUN wget http://archives.fedoraproject.org/pub/archive/epel/5/x86_64/epel-release-5-4.noarch.rpm 
RUN rpm -Uvh epel-release-5-4.noarch.rpm
RUN rpm -Uvh http://rpms.remirepo.net/enterprise/remi-release-5.rpm
RUN yum -y upgrade

# setup tools
RUN yum install -y git make gcc gcc-c++ openssl openssl-devel readline-devel ftp unzip libxml2-devel libxslt-devel memcached
RUN yum install -y ImageMagick6 ImageMagick6-devel ImageMagick6-c++ ImageMagick6-c++-devel --enablerepo=remi

# setup mysql 5.5.54-1
RUN yum install -y --enablerepo=remi mysql-server mysql-devel.x86_64 

# setup ruby
RUN wget http://ftp.ruby-lang.org/pub/ruby/1.8/ruby-1.8.7-p330.tar.gz
RUN tar zxvf ruby-1.8.7-p330.tar.gz
RUN cd ruby-1.8.7-p330 && ./configure --prefix=/usr && make && make install

# setup rubygems
RUN wget http://rubygems.org/rubygems/rubygems-1.3.6.zip
RUN unzip rubygems-1.3.6.zip
RUN cd rubygems-1.3.6 && ruby setup.rb

RUN gem install specific_install --no-ri --no-rdoc
RUN gem install rake -v=0.8.7 --no-ri --no-rdoc
RUN gem install rails -v=2.3.4 --no-ri --no-rdoc
RUN gem install mime-types -v=1.19 --no-ri --no-rdoc
RUN gem install rmagick -v=2.13.2 --no-ri --no-rdoc
RUN gem install nokogiri -v=1.5.10 --no-ri --no-rdoc
RUN gem install json_pure -v=1.8.3 --no-ri --no-rdoc
RUN gem install json -v=1.7.3 --no-ri --no-rdoc
RUN gem install daemons -v=1.0.10 --no-ri --no-rdoc
RUN gem install gettext -v=2.1.0 --no-ri --no-rdoc
RUN gem install hoe -v=2.3.3 --no-ri --no-rdoc
RUN gem install hpricot -v=0.8.2 --no-ri --no-rdoc
RUN gem install builder -v=3.0.0 --no-ri --no-rdoc
RUN gem install xml-simple -v=1.1.2 --no-ri --no-rdoc
RUN gem install rdoc -v=3.12 --no-ri --no-rdoc
RUN gem install net-ssh -v=2.9.2 --no-ri --no-rdoc
RUN gem install net-sftp -v=2.1.2 --no-ri --no-rdoc
RUN gem install ruby-debug -v=0.10.4 --no-ri --no-rdoc
RUN gem install mysql -v=2.8.1 --no-ri --no-rdoc
