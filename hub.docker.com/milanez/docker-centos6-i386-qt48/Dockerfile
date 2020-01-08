FROM toopher/centos-i386:centos6

RUN echo -e "[PUIAS_6_core_Base]\nname=PUIAS core Base \$releasever - \$basearch\nmirrorlist=http://puias.math.ias.edu/data/puias/computational/\$releasever/\$basearch/mirrorlist\nenabled=1\ngpgcheck=0\ngpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-puias\n" > /etc/yum.repos.d/puias.repo && cat /etc/yum.repos.d/puias.repo

RUN yum --skip-broken groupinstall -y 'Development Tools'  || true
RUN yum install -y wget tar glibc-devel.i686 openssl-devel libstdc++-devel || true
RUN yum install -y qt48-devel || true
RUN yum install -y openssl openssl-devel || true
