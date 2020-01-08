# centos7
FROM centos:7.2.1511

# author
MAINTAINER Wim Li <liwangmj@gmail.com> (http://liwangmj.com)

# copy
ADD gperftools-2.5.tar.gz /tmp/
ADD fcgiwrap-1.1.0.tar.gz /tmp/
ADD libiconv-1.13.1.tar.gz /tmp/
ADD unixODBC-2.3.4.tar.gz /tmp/
ADD openssl-OpenSSL_1_0_2j.tar.gz /tmp/
COPY sslconfig-master.zip /tmp/
COPY Centos-7.repo /etc/yum.repos.d/CentOS-Base.repo

# update
RUN set -x \
    && sed -i.backup 's/^enabled=1/enabled=0/' /etc/yum/pluginconf.d/fastestmirror.conf \
    && echo '==> epel' \
    && yum -y install epel-release \
    && echo '==> install basic' \
    && yum -y install aclocal autoconf aotuheader automake libtool pkgconfig make cmake gcc gcc-c++ libstdc++-static glibc glibc-devel bind-utils net-tools tar unzip wget patch lsof jq nc perl perl-devel perl-CPAN lua lua-devel luajit luajit-devel luarocks python python-devel fcgi fcgi-devel spawn-fcgi jemalloc jemalloc-devel libunwind libunwind-devel zlib zlib-devel bzip2 bzip2-devel curl curl-devel \
    && echo '==> install setuptools' \
    && yum -y install python-setuptools python-pip \
    && echo '==> install supervisor schedule devcron' \
    && easy_install supervisor \
    && pip2 install schedule devcron \
    && echo_supervisord_conf > /etc/supervisord.conf \
    && echo '==> install openssl' \
    && cd /tmp \
    && unzip sslconfig-master.zip \
    && chmod 755 -R openssl-OpenSSL_1_0_2j \
    && cd openssl-OpenSSL_1_0_2j \
    && patch -p1 < /tmp/sslconfig-master/patches/openssl__chacha20_poly1305_draft_and_rfc_ossl102j.patch \
    && ./config shared zlib-dynamic enable-camellia \
    && make -j4 \
    && make install \
    && ln -sf /usr/local/ssl/bin/openssl /usr/bin/openssl \
    && ln -sf /usr/local/ssl/include/openssl /usr/include/openssl \
    && ln -sf /usr/local/ssl/lib/libssl.so /usr/lib64/libssl.so \
    && ln -sf /usr/local/ssl/lib/libcrypto.so /usr/lib64/libcrypto.so \
    && ln -sf /usr/local/ssl/lib/libssl.so.1.0.0 /usr/lib64/libssl.so.10 \
    && ln -sf /usr/local/ssl/lib/libcrypto.so.1.0.0 /usr/lib64/libcrypto.so.10 \
    && ln -sf /usr/local/ssl/lib/libssl.so.1.0.0 /usr/lib64/libssl.so.1.0.0 \
    && ln -sf /usr/local/ssl/lib/libcrypto.so.1.0.0 /usr/lib64/libcrypto.so.1.0.0 \
    && cp -rfp /usr/local/ssl/lib/pkgconfig/* /usr/lib64/pkgconfig/ \
    && echo '==> install tcmalloc' \
    && cd /tmp \
    && chmod 755 -R gperftools-2.5 \
    && cd gperftools-2.5 \
    && ./configure \
    && make -j4 \
    && make install \
    && echo '==> install fcgiwrap' \
    && cd /tmp \
    && chmod 755 -R fcgiwrap-1.1.0 \
    && cd fcgiwrap-1.1.0 \
    && autoreconf -i \
    && ./configure \
    && make -j4 \
    && make install \
    && echo '==> install libiconv' \
    && cd /tmp \
    && chmod 755 -R libiconv-1.13.1 \
    && cd libiconv-1.13.1 \
    && ./configure \
    && make \
    && make install \
    && echo '==> install unixodbc' \
    && cd /tmp \
    && chmod 755 -R unixODBC-2.3.4 \
    && cd unixODBC-2.3.4 \
    && ./configure \
    && make -j4 \
    && make install \
    && echo '==> setlocale' \
    && localedef -c -i en_US -f UTF-8 en_US.UTF-8 \
    && echo '==> config ld.so.conf' \
    && echo '.' > /etc/ld.so.conf.d/local.conf \
    && echo '/usr/local/lib' >> /etc/ld.so.conf.d/local.conf \
    && echo '/usr/local/lib64' >> /etc/ld.so.conf.d/local.conf \
    && ldconfig -v \
    && echo '==> useradd www' \
    && groupadd www \
    && useradd -G www -g www --no-create-home www \
    && mkdir -p /www \
    && chown www:www -R /www \
    && echo '==> clean' \
    && yum clean all \
    && rm -rf /tmp/*

# workdir
WORKDIR /opt/persistent_data
VOLUME ["/opt/persistent_data"]

# env
ENV LD_LIBRARY_PATH .:/usr/local/lib:/usr/local/lib64
ENV PKG_CONFIG_PATH /usr/local/lib/pkgconfig
ENV PERSISTENT_DATA /persistent_data
ENV PATH $PERSISTENT_DATA:$PATH

# port
EXPOSE 65533

# cmd
CMD ["/usr/sbin/init"]