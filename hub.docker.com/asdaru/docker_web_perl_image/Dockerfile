# web image for perl site with imageMagick
#
# @version 	0.2
# @author 	asda <asda@asda.ru>
FROM ubuntu:16.04

MAINTAINER asda.ru


RUN apt-get update && \
	apt-get install -y \
		rsyslog \
		libmysqlclient-dev \
		wget \
		libdbd-mysql-perl libssl-dev \
		gcc g++ libncurses5-dev libtool make \
		libxml2-dev libperl-dev \
		libexpat1-dev \
		libgd2-dev \
		libtiff-dev libfreetype6-dev libbz2-dev libpng12-dev libwmf-dev libjasper-dev liblcms2-dev libgs-dev \
		locales \
		tzdata
		
RUN locale-gen en_US.UTF-8 \
	&& ln -snf /usr/share/zoneinfo/Europe/Moscow /etc/localtime \
	&& dpkg-reconfigure -f noninteractive tzdata

ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8 
			
		
RUN cpan Archive::Zip \ 
			&& cpan Barcode::Code128 \ 
			&& cpan DBI \
			&& cpan DBD:mysql \ 
			&& cpan HTTP::Date \
			&& cpan UUID::Tiny \
			&& cpan Crypt::CBC \
			&& cpan JSON \
			&& cpan Switch \
			&& cpan Time::Local \
			&& cpan POSIX::strptime \
			&& cpan Crypt::DES \
			&& cpan Capture::Tiny \
			&& cpan Image::Size \
			&& cpan Data::UUID \
			&& cpan experimental \
			&& cpan IO::Socket::IP \
			&& cpan App::cpanminus \
			&& cpanm GD \
			&& cpan Image::Resize \ 
			&& cpan List::Util \
			&& cpan Digest::SHA1 \ 
			&& cpan HTTP::Date \
			&& cpan MIME::EncWords \ 
			&& cpan MIME::Lite \
			&& cpan XML::Simple \
			&& cpan Net::LDAP \
			&& cpan AnyEvent::DBI::MySQL \ 
			&& cpan EV \
			&& cpan GD::Barcode \ 
			&& cpan IO::Socket::PortState \
			&& apt-get install -y libfontconfig1 libxrender1 libxext-dev netcat




RUN 	cd /tmp && \
		wget ftp://ftp.imagemagick.org/pub/ImageMagick/ImageMagick.tar.gz && \
		tar xfz ImageMagick.tar.gz && \
		cd ImageMagick-7.0.* && \
		./configure --with-perl=yes --prefix=/usr && \
		make install 

		
RUN apt-get clean && \
	rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /root/.cpan	


