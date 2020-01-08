FROM centos:latest

MAINTAINER Erik Velasquez <erikv@biwiser.com>

#initial config
RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm

#Install Apache
RUN yum install -y nginx
RUN systemctl enable nginx
RUN yum install firewalld -y


#Install Remi Release
RUN yum -y install epel-release
#RUN rpm -Uvh http://rpms.remirepo.net/enterprise/remi-release-7.rpm
RUN yum -y install yum-utils
RUN yum -y install unzip wget
RUN yum update -y

#Install Php 7.2
RUN yum install -y yum-utils
RUN yum-config-manager --enable remi-php72
RUN yum install -y php php-mcrypt php-cli php-gd php-curl php-mysql php-ldap php-zip php-fileinfo php-pgsql php-fpm php-mbstring php-xml

#enable PHP-FPM service
RUN systemctl enable php-fpm

#install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
#RUN mv composer.phar /usr/local/bin/composer


# Install Machine Learning Server

# Install Developments tools
#RUN yum groupinstall -y 'Development Tools'
RUN yum install -y gcc gcc-c++ make
RUN yum install -y unixODBC-devel openssl-devel libxml2-devel mysql-devel postgresql-devel 

# Import the Microsoft repository key
RUN rpm --import https://packages.microsoft.com/keys/microsoft.asc
# Create local `azure-cli` repository
RUN sh -c 'echo -e "[azure-cli]\nname=Azure CLI\nbaseurl=https://packages.microsoft.com/yumrepos/azure-cli\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/azure-cli.repo'
# Set the location of the package repo at the "prod" directory
# The following command is for version 7.x
# For 6.x, replace 7 with 6 to get that version
# On RHEL 7:
RUN rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm
# Update packages on your system:
RUN yum update -y

# Install the server
# The following command is for version 7.x
# For 6.x: yum install microsoft-mlserver-el6-9.3.0
#RUN yum install -y microsoft-mlserver-all-9.3.0

# Activate the server
#RUN /opt/microsoft/mlserver/9.3.0/bin/R/activate.sh

# Slim down the container
#RUN yum clean all

# List installed packages as a verification step
#RUN rpm -qa | grep microsoft

# Choose a package name and obtain verbose version information
#RUN rpm -qi microsoft-mlserver-packages-r-9.3.0

# Install R client 3.4.3
RUN yum install -y microsoft-r-client-packages-3.4.3

#End Install Machine Learnig Server

#Install R dependencies
COPY packages.R /tmp/
RUN Rscript /tmp/packages.R


# Slim down the container
RUN yum clean all
