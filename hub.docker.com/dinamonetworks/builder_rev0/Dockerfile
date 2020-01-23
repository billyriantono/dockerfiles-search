FROM centos:7.4.1708

LABEL version=0.1
LABEL description="builder env for HSM Rev0"
LABEL maintainer="eniltonj@dinamonetworks.com"

RUN yum install -y \
        gcc gcc-c++ \
        vim \
        net-tools \
        git \
        ntp \
        libtar libtar-devel \
        libusb libusb-devel \
        newt newt-devel \
        libtool-ltdl \
        libtool-ltdl-devel \
        sqlite sqlite-devel \
        crda \
        wget \
        make \
        rpm \
        rpm-devel \
        rpm-build \
        zlib zlib-devel \
        bison \
        flex doxygen \
        flex automake \
        flex libtool \
        net-tools \
        \
        bzip2-devel \
        elfutils-devel \
        elfutils-libelf-devel \
        perl-devel \
        perl \
        python-devel \
        python-setuptools \
        chrpath \
        mysql-devel \
        lm_sensors-devel \
        tcp_wrappers-devel \
        perl-ExtUtils-Embed \
        \
        gnutls-devel \
        nss-devel \
        nspr-devel \
        gettext-devel \
        \
        libxslt libxslt-devel \
        libxml2 libxml2-devel \
        \
        openssl-devel \
        cpan \
        patch \
        autoconf \
        automake \
        libtool

# yum installs a diferent source version of the kernel we use in
# the appliances, so we use rpm to install the exact version we need.

RUN rpm -ivh http://vault.centos.org/7.4.1708/os/x86_64/Packages/kernel-devel-3.10.0-693.el7.x86_64.rpm

RUN rpm -ivh --nodeps http://vault.centos.org/7.4.1708/os/x86_64/Packages/kernel-3.10.0-693.el7.x86_64.rpm

# yes, there are two lines for IO:Socket::SSL

ENV PERL_MM_USE_DEFAULT=1
RUN cpan -i IO::Socket::SSL ; exit 0
RUN cpan -i IO::Socket::SSL && \
    cpan -i Test::More

WORKDIR /usr/src
COPY [  "install_openssl_102c.sh", \
        "install_openslp_102c.sh" , \
        "install_net-snmp_102c.sh", \
        "install_xmlsec_102c.sh", \
        "install_openssl_111a.sh", \
        "install_openslp_111a.sh" , \
        "install_net-snmp_111a.sh", \
        "install_xmlsec_111a.sh", \
        "./" ]

# these commands may be agglutinated in one run with && (economy of 100MB)
RUN ./install_openssl_102c.sh
RUN ./install_openslp_102c.sh
RUN ./install_net-snmp_102c.sh
RUN ./install_xmlsec_102c.sh

RUN ./install_openssl_111a.sh
RUN ./install_openslp_111a.sh
RUN ./install_net-snmp_111a.sh
RUN ./install_xmlsec_111a.sh

WORKDIR /root
COPY [  ".bashrc", \
        ".git-prompt.sh", \
        ".gitconfig", \
        ".sqliterc", \
        ".tcshrc", \
        ".viminfo", \
        ".vimrc", \
        ".bash_profile", \
        "./" ]

ENV USER root
ENV USERNAME root

RUN sed  "s/di=0;35/di=1;37/" -i /root/.bashrc ; \
    sed '2a colorscheme blue' -i /root/.vimrc

# faking the kernel version... (for fw build purposes)
WORKDIR /usr/bin
RUN mv uname uname.ORIGINAL
COPY uname .

# clearing stuff
WORKDIR /usr/src

# Ports: API, Webcon, SLP, KMIP. MI, SNMP(Get)

EXPOSE 4433
EXPOSE 443
EXPOSE 427
EXPOSE 5696
EXPOSE 3344
EXPOSE 161/udp

RUN yum clean all &&\
    rm -rf /var/cache/yum &&\
    rm -rf openssl-1.1.1a &&\
    rm -rf openssl-1.0.2c &&\
    rm -rf openssl-1.0.2c.tar.gz &&\
    rm -rf openssl-1.1.1a.tar.gz &&\
    \
    rm -rf openslp-2.0.0-6.el7.src.rpm &&\
    rm -rf openslp-2.0.0-7.el7_5 &&\
    \
    rm -rf net-snmp-5.7.2-28.el7.src.rpm &&\
    rm -rf net-snmp-5.8 &&\
    rm -rf net-snmp-5.8.tar.gz &&\
    \
    rm -rf xmlsec1-1.2.20-5.el7.src.rpm &&\
    rm -rf xmlsec1-1.2.25 &&\
    rm -rf xmlsec1-1.2.25.tar.gz &&\
    rm -rf xmlsec1-1.2.27 &&\
    \
    rm -rf /root/rpmbuild/RPMS/x86_64
