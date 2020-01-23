FROM centos

RUN rpm --import https://www.centos.org/keys/RPM-GPG-KEY-CentOS-7
RUN rpm --import https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7
RUN rpm --import https://dl.fedoraproject.org/pub/epel/RPM-GPG-KEY-EPEL-7Server
RUN yum -y install epel-release --nogpgcheck
RUN rpm --import https://rpms.remirepo.net/RPM-GPG-KEY-remi
RUN rpm --import https://rpms.remirepo.net/RPM-GPG-KEY-remi2017
RUN rpm --import https://rpms.remirepo.net/RPM-GPG-KEY-remi2018
RUN rpm --import https://rpms.remirepo.net/RPM-GPG-KEY-remi2019
RUN yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm --nogpgcheck
RUN yum -y update
RUN yum -y install yum-utils --nogpgcheck
RUN yum-config-manager --enable remi-php56 --nogpgcheck
RUN yum -y install httpd httpd_tools openssl mod_ssl psmisc php php-bcmath php-cli php-common php-gd php-imap php-intl php-mbstring php-mcrypt php-mysqlnd php-pdo php-pecl-imagick php-pecl-jsonc php-pecl-zip php-soap php-xml php-xdebug cronie cronie-anacron crontabs --nogpgcheck
RUN yum clean all

RUN mkdir -p /opt/landgorilla/bash_docker/

COPY ./configs/httpd.conf /etc/httpd/conf/httpd.conf
COPY ./bash/resodata.sh /opt/landgorilla/bash_docker/resodata.sh
COPY ./bash/privileged.sh /opt/landgorilla/bash_docker/privileged.sh

RUN chmod +x /opt/landgorilla/bash_docker/resodata.sh
RUN chmod +x /opt/landgorilla/bash_docker/privileged.sh

RUN /opt/landgorilla/bash_docker/resodata.sh
RUN /opt/landgorilla/bash_docker/privileged.sh

ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]
