FROM centos
RUN yum install -y \
        ruby-devel \
 	gcc \
 	make \
	rpm-build \
 	rubygems \
	wget \
	git \
	gettext \ 
	&& yum clean all
RUN gem install --no-ri --no-rdoc fpm

