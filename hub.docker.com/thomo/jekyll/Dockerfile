FROM centos:7

MAINTAINER Thomas Mohaupt "Thomas.Mohaupt@gmail.com"

RUN echo "deltarpm=0" >> /etc/yum.conf
RUN rpm --import  /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

ENV BUILD_DATE=2015-08-24

RUN yum -y install \
				epel-release \
				gcc \
				make \
				ruby \
				ruby-devel

# install from epel repository
RUN yum -y install \				
				nodejs 

RUN gem install jekyll -N

EXPOSE 4000

WORKDIR /data

ENTRYPOINT ["jekyll"]

CMD ["serve", "--host=0.0.0.0", "--force_polling"]