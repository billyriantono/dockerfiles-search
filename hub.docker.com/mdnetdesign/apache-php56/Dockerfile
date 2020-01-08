FROM mdnetdesign/apache

RUN yum -y install epel-release
RUN rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm

RUN yum -y install php56w php56w-common php56w-mysql php56w-pdo
RUN yum -y install php56w-xml php56w-intl php56w-cli php56w-mbstring
RUN yum -y install php56w-pecl-xdebug php56w-imap php56w-gd php56w-opcache

RUN sed -ri "s/max_execution_time\s*=\s*[0-9]+/max_execution_time=300/" /etc/php.ini
RUN sed -ri "s/short_open_tag\s*=\s*[Oo]ff/short_open_tag=On/" /etc/php.ini
RUN sed -ri "s/post_max_size\s*=\s*[0-9]+M/post_max_size=1G/" /etc/php.ini
RUN sed -ri "s/upload_max_filesize\s*=\s*[0-9]+M/upload_max_filesize=200M/" /etc/php.ini
RUN sed -ri "s/memory_limit\s*=\s*[0-9]+M/memory_limit=1G/" /etc/php.ini
