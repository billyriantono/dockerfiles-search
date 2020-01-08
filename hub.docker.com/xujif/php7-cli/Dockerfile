FROM centos:6
MAINTAINER xujif <i@xujif.com>
RUN rpm -Uvh https://mirror.webtatic.com/yum/el6/latest.rpm
RUN rpm -Uvh http://mirrors.hust.edu.cn/epel//5/x86_64/epel-release-5-4.noarch.rpm
RUN yum update -y
RUN yum install -y php70w \
					php70w-bcmath \
					php70w-cli \
					php70w-common \
					php70w-gd \ 
					php70w-mbstring \
					php70w-mcrypt \ 
					php70w-mysqlnd \ 
					php70w-opcache \
					php70w-pdo \ 
					php70w-pear \ 
					php70w-pgsql \ 
					php70w-process \   
					php70w-soap \
					php70w-tidy \
					php70w-xml
RUN yum clean all
ADD mongodb.so /usr/lib64/php/modules/
ADD mongodb.ini /etc/php.d/

ENTRYPOINT  ["/usr/bin/php"]
