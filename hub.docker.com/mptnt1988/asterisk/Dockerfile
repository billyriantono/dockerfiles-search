FROM centos/systemd
MAINTAINER "Tuan Tran" <mptnt1988@gmail.com>
ENV mysql_secure_installation_auto /usr/scripts/mysql_secure_installation_auto.sh
COPY mysql_secure_installation_auto.sh /usr/scripts/
# Update system
RUN yum -y update
# Install dev tools
RUN yum -y groupinstall core base "Development Tools"
# Add the asterisk user
RUN adduser asterisk -m -c "Asterisk User"
# Install dependencies
RUN yum -y install lynx tftp-server unixODBC mysql-connector-odbc \
      mariadb-server mariadb httpd ncurses-devel sendmail sendmail-cf sox \
      newt-devel libxml2-devel libtiff-devel audiofile-devel gtk2-devel \
      subversion kernel-devel git crontabs cronie cronie-anacron wget vim \
      uuid-devel sqlite-devel net-tools gnutls-devel python-devel texinfo \
      libuuid-devel
# Install php5.6w
RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm && \
    yum remove php* && \
    yum -y install php56w php56w-pdo php56w-mysql php56w-mbstring php56w-pear \
    php56w-process php56w-xml php56w-opcache php56w-ldap php56w-intl php56w-soap
# Install NodeJS
RUN curl -sL https://rpm.nodesource.com/setup_8.x | bash - && \
    yum install -y nodejs
# Enable and Start MariaDB
RUN systemctl enable mariadb.service
RUN $mysql_secure_installation_auto
# Enable and Start Apache
RUN systemctl enable httpd.service
# Install Dependencies for Google Voice iksemel
WORKDIR /usr/src
RUN wget https://github.com/meduketto/iksemel/archive/master.zip -O iksemel-master.zip && \
    unzip iksemel-master.zip && \
    rm -f iksemel-master.zip && \
    cd iksemel-master && \
    ./autogen.sh && \
    ./configure && \
    make && \
    make install
# INSTALL & CONFIGURE ASTERISK
WORKDIR /usr/src
RUN wget http://downloads.asterisk.org/pub/telephony/asterisk/asterisk-14-current.tar.gz && \
    wget -O jansson.tar.gz https://github.com/akheron/jansson/archive/v2.10.tar.gz
# Compile and Install jansson
WORKDIR /usr/src
RUN tar vxfz jansson.tar.gz && \
    rm -f jansson.tar.gz && \
    cd jansson-* && \
    autoreconf -i && \
    ./configure --libdir=/usr/lib64 && \
    make && \
    make install
# Compile and install Asterisk
WORKDIR /usr/src
RUN tar xvfz asterisk-14-current.tar.gz && \
    rm -f asterisk-14-current.tar.gz && \
    cd asterisk-* && \
    contrib/scripts/install_prereq install && \
    ./configure --libdir=/usr/lib64 --with-pjproject-bundled && \
    contrib/scripts/get_mp3_source.sh && \
    make menuselect.makeopts && \
    menuselect/menuselect \
      --enable format_mp3 \
      menuselect.makeopts && \
    make && \
    make install && \
    make config && \
    ldconfig && \
    chkconfig asterisk off
# Set Asterisk ownership permissions
RUN chown asterisk. /var/run/asterisk && \
    chown -R asterisk. /etc/asterisk && \
    chown -R asterisk. /var/{lib,log,spool}/asterisk && \
    chown -R asterisk. /usr/lib64/asterisk && \
    chown -R asterisk. /var/www/
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]
