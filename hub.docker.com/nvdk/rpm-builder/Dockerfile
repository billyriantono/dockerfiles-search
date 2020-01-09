FROM centos:7
MAINTAINER "Niels Vandekeybus" <niels.vandekeybus@tenforce.com>
RUN yum -y install git gcc gmake autoconf net-tools automake libtool flex openssl bison gperf gawk m4 make openssl-devel readline-devel wget rpm-build redhat-rpm-config
ADD build-rpms.sh /usr/bin/
RUN chmod +x /usr/bin/build-rpms.sh
ENTRYPOINT ["/usr/bin/build-rpms.sh"]
