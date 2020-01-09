FROM centos:7
MAINTAINER billypon

# init
RUN cp -f /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    useradd www

# install
RUN yum install -y epel-release yum-utils make gcc autoconf automake && \

    # fcgiwrap
    yum install -y fcgi fcgi-devel && \
    curl -sL https://github.com/gnosek/fcgiwrap/tarball/master | tar zx -C /tmp && \
    cd /tmp/gnosek-fcgiwrap-* && autoreconf -i && ./configure && make && make install && \
    rm -rf /tmp/gnosek-fcgiwrap-* && \

    # spawn-fcgi
	yum install -y spawn-fcgi && \
    curl -sL https://github.com/lighttpd/spawn-fcgi/tarball/master | tar zx -C /tmp && \
    cd /tmp/lighttpd-spawn-fcgi-*/src && \
    sed -i 'N;/\n.*I will not set/!P;D' spawn-fcgi.c && sed -i '/I will not/{n;d}' spawn-fcgi.c && sed -i '/I will not/{n;d}' spawn-fcgi.c && sed -i '/I will not/d' spawn-fcgi.c && \
	cd .. && \
    ./autogen.sh && ./configure && make && cp src/spawn-fcgi /usr/bin/ && \
    rm -rf /tmp/gnosek-fcgiwrap-* && \
    chkconfig spawn-fcgi on && \

    # php
    yum install -y php php-fpm php-devel \
                   php-bcmath php-gd php-json php-mbstring php-mcrypt php-xml php-xmlrpc php-soap \
                   php-mysql php-pecl-redis \
                   ImageMagick php-pecl-imagick && \
    sed -i "/PrivateTmp/d" /usr/lib/systemd/system/php-fpm.service && \

    # php eaccelerator
    curl -sL https://github.com/eaccelerator/eaccelerator/tarball/master | tar zx -C /tmp && \
    cd /tmp/eaccelerator-* && phpize && ./configure && make && make install && \
    rm -rf /tmp/eaccelerator-* && \

    # php zend guard loader
    curl -sL http://downloads.zend.com/guard/6.0.0/ZendGuardLoader-70429-PHP-5.4-linux-glibc23-x86_64.tar.gz | tar zx -C /tmp && \
    cd /tmp/ZendGuardLoader-*/php-* && cp ZendGuardLoader.so /usr/lib64/php/modules && \
    rm -rf /tmp/ZendGuardLoader-* && \

    # redis
    yum install -y redis && \
    gpasswd -a redis www && \

    # node
    curl -sL https://rpm.nodesource.com/setup_6.x | bash && \
    yum install -y nodejs && \

    # dotnet(/usr/lib/dotnet)

    # mono
    rpm --import "http://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF" && \
    yum-config-manager --add-repo http://download.mono-project.com/repo/centos/ && \
    yum install -y mono xsp && \

    # sendmail
    yum install -y sendmail && \
    echo 'LC_ALL="POSIX"' >> /etc/locale.conf && \

    # clean
    yum autoremove -y epel-release yum-utils make gcc autoconf automake fcgi-devel php-devel && \
    yum autoremove -y && \
    yum clean all

# system
RUN rm -f /etc/systemd/system/multi-user.target.wants/{sendmail,sm-client}.service && \
    for x in `echo init php-fpm redis`; do ln -s /usr/lib/systemd/system/${x}.service /etc/systemd/system/multi-user.target.wants/; done

ENTRYPOINT ["/sbin/init"]
